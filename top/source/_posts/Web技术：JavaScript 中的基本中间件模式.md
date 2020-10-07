
title: Web技术：JavaScript 中的基本中间件模式
author: 知识铺
date: 2020-10-07 18:15:14
tags: 
---
 有没有想过流行的网络框架中的中间件，如快递或[Koa，是如何工作的](https://zshipu.com/t?url=https://koajs.com/)？

在 Express 中，我们有具有此签名的中间件功能：

 <code>const middleare = (req, res, next) => {
  // do stuff
  next()
}</code> 

在 Koa 中，我们有这样：

 <code>const middleware = (ctx, next) => {
  // do stuffs
  next()
}</code> 

基本上，您有一些对象（对于 Express 或 Koa）和一个函数作为中间件函数的参数。调用时，将调用下一个中间件函数。如果修改当前中间件函数中的参数对象，则下一个中间件将接收这些修改的对象。例如：```req``````res``````ctx``````next()``````next()```

 <code>// Middleware usage in Koa

app.use((ctx, next) => {
  ctx.name = 'Doe'
  next()
})

app.use((ctx, next) => {
  console.log(ctx.name) // will log `Doe`
})

app.use((ctx, next) => {
  // this will not get invoked
})</code> 

如果不调用该函数，则执行将停止，并且不会调用下一个中间件函数。```next()```

## [](#implementation)实现

那么，如何实现这样的模式呢？具有 30 行 JavaScript：

 <code>function Pipeline(...middlewares) {
  const stack = middlewares

  const push = (...middlewares) => {
    stack.push(...middlewares)
  }

  const execute = async (context) => {
    let prevIndex = -1

    const runner = async (index) => {
      if (index === prevIndex) {
        throw new Error('next() called multiple times')
      }

      prevIndex = index

      const middleware = stack[index]

      if (middleware) {
        await middleware(context, () => {
          return runner(index + 1)
        })
      }
    }

    await runner(0)
  }

  return { push, execute }
}</code> 

中间件模式的实现与 Koa 几乎相同。如果您想了解 Koa 是如何执行的，请查看[```koa-compose 包的```](https://zshipu.com/t?url=https://github.com/koajs/compose/blob/master/index.js#L31-L47)源代码。

## [](#usage)使用

让我们看一个使用它的示例：

 <code>// create a middleware pipeline
const pipeline = Pipeline(
  // with an initial middleware
  (ctx, next) => {
    console.log(ctx)
    next()
  }
)

// add some more middlewares
pipeline.push(
  (ctx, next) => {
    ctx.value = ctx.value + 21
    next()
  },
  (ctx, next) => {
    ctx.value = ctx.value * 2
    next()
  }
)

// add the terminating middleware
pipeline.push((ctx, next) => {
  console.log(ctx)
  // not calling `next()`
})

// add another one for fun ¯\_(ツ)_/¯
pipeline.push((ctx, next) => {
  console.log('this will not be logged')
})

// execute the pipeline with initial value of `ctx`
pipeline.execute({ value: 0 })</code> 

如果你运行那段代码，你能猜出输出是什么吗？是的， 你猜对了：

 <code>{ value: 0 }
{ value: 42 }</code> 

顺便说一下，这绝对可以与异步中间件功能太。

## [](#typescript)类型脚本

现在， 给它一些类型脚本的爱怎么样？

 <code>type Next = () => Promise<void> | void

type Middleware<T> = (context: T, next: Next) => Promise<void> | void

type Pipeline<T> = {
  push: (...middlewares: Middleware<T>[]) => void
  execute: (context: T) => Promise<void>
}

function Pipeline<T>(...middlewares: Middleware<T>[]): Pipeline<T> {
  const stack: Middleware<T>[] = middlewares

  const push: Pipeline<T>['push'] = (...middlewares) => {
    stack.push(...middlewares)
  }

  const execute: Pipeline<T>['execute'] = async (context) => {
    let prevIndex = -1

    const runner = async (index: number): Promise<void> => {
      if (index === prevIndex) {
        throw new Error('next() called multiple times')
      }

      prevIndex = index

      const middleware = stack[index]

      if (middleware) {
        await middleware(context, () => {
          return runner(index + 1)
        })
      }
    }

    await runner(0)
  }

  return { push, execute }
}</code> 

键入所有内容后，现在可以声明特定中间件管道的上下文对象类型，例如：

 <code>type Context = {
  value: number
}

const pipeline = Pipeline<Context>()</code> 

* * *

