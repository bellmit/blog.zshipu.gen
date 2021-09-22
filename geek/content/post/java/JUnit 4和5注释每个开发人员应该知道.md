
---
title: JUnit 4和5注释每个开发人员应该知道
author: 知识铺
date: 2021-02-25 20:32:12+08:00
tags: []
---
# [](#a-summary-of-junit-4-amp-5-annotations-with%C2%A0examples)<font _mstmutation="1" _msthash="288184" _msttexthash="75491351">JUnit 4 +5 注释摘要，附有示例</font>

<font _mstmutation="1" _msthash="275951" _msttexthash="168596467">在写这篇文章之前，我只知道一些常用的JUnit 4注释，如</font>

```
@RunWith 
@Test
@Before
@After
@BeforeClass
@AfterClass
```

<font _mstmutation="1" _msthash="276523" _msttexthash="234328835">你不得不评论多少次测试？令我吃惊的是，有注释可以做到这一点。</font>

```
@Ignore("Reason for ignoring")
@Disabled("Reason for disabling")
```

嗯，事实证明，还有其他一些注释，特别是在JUnit 5，可以帮助编写更好和更有效的测试。

* * *

## [](#what-to%C2%A0expect)<font _mstmutation="1" _msthash="290849" _msttexthash="19248814">期待什么？</font>

在本文中，我将用用例来涵盖以下注释。本文的目的是向您介绍注释，它不会进入每个注释的更大细节。

*_本文的所有示例也可在 Github 中找到。请查看以下存储库。*_

## ![GitHub logo](https://res.cloudinary.com/practicaldev/image/fetch/s--vJ70wriM--/c_limit%2Cf_auto%2Cfl_progressive%2Cq_auto%2Cw_880/https://practicaldev-herokuapp-com.freetls.fastly.net/assets/github-logo-ba8488d21cd8ee1fee097b8410db9deaa41d0ca30b004c0c63de0a479114156f.svg) <font _mstmutation="1" _msthash="690508" _msttexthash="46003438">[哈米迪](https://zshipu.com/t?url=https://github.com/rhamedy)/[朱尼特注释 - 示例](https://zshipu.com/t?url=https://github.com/rhamedy/junit-annotations-examples)</font>

### JUnit 4 和 5 注释与示例

本文的目标受众是任何级别的开发人员。

[![Alt Text](https://res.cloudinary.com/practicaldev/image/fetch/s--pEBw2UxZ--/c_limit%2Cf_auto%2Cfl_progressive%2Cq_auto%2Cw_880/https://thepracticaldev.s3.amazonaws.com/i/lutifty7vsbuxrz4nqwu.png)](https://zshipu.com/t?url=https://res.cloudinary.com/practicaldev/image/fetch/s--pEBw2UxZ--/c_limit%2Cf_auto%2Cfl_progressive%2Cq_auto%2Cw_880/https://thepracticaldev.s3.amazonaws.com/i/lutifty7vsbuxrz4nqwu.png)

### [](#junit-4)<font _mstmutation="1" _msthash="305266" _msttexthash="5232864">JUnit 4</font>

以下[JUnit 4](https://zshipu.com/t?url=https://github.com/junit-team/junit4)注释将包括

[![Alt Text](https://res.cloudinary.com/practicaldev/image/fetch/s--MMIdq81B--/c_limit%2Cf_auto%2Cfl_progressive%2Cq_auto%2Cw_880/https://thepracticaldev.s3.amazonaws.com/i/4cp8t1zggjoyt4p6r7yv.png)](https://zshipu.com/t?url=https://res.cloudinary.com/practicaldev/image/fetch/s--MMIdq81B--/c_limit%2Cf_auto%2Cfl_progressive%2Cq_auto%2Cw_880/https://thepracticaldev.s3.amazonaws.com/i/4cp8t1zggjoyt4p6r7yv.png)

### [](#junit-5)<font _mstmutation="1" _msthash="306202" _msttexthash="5232981">JUnit 5</font>

以下[JUnit 5](https://zshipu.com/t?url=https://github.com/junit-team/junit5)注释用示例进行解释

[![Alt Text](https://res.cloudinary.com/practicaldev/image/fetch/s--_VuFZ0cJ--/c_limit%2Cf_auto%2Cfl_progressive%2Cq_auto%2Cw_880/https://thepracticaldev.s3.amazonaws.com/i/53m3mi7b0ds4gzld9lik.png)](https://zshipu.com/t?url=https://res.cloudinary.com/practicaldev/image/fetch/s--_VuFZ0cJ--/c_limit%2Cf_auto%2Cfl_progressive%2Cq_auto%2Cw_880/https://thepracticaldev.s3.amazonaws.com/i/53m3mi7b0ds4gzld9lik.png)

* * *

## [](#junit-dependencies)<font _mstmutation="1" _msthash="304668" _msttexthash="12315017">JUnit依赖</font>

<font _mstmutation="1" _msthash="291499" _msttexthash="145519972">本文中的所有示例都使用以下 JUnit 依赖项进行测试。</font>

```
testImplementation 'org.junit.jupiter:junit-jupiter-api:5.3.1'
testRuntimeOnly 'org.junit.jupiter:junit-jupiter-engine:5.3.1'
testCompileOnly 'junit:junit:4.12'
testRuntimeOnly 'org.junit.vintage:junit-vintage-engine:5.3.1'
```

有关详细信息，请查看 Github[存储库](https://zshipu.com/t?url=https://github.com/rhamedy/junit-annotations-examples)。

* * *

# [](#junit-annotations-usage)<font _mstmutation="1" _msthash="306267" _msttexthash="20929545">JUnit注释使用</font>

让我们用简短的使用示例逐一探索 JUnit 4 注释

## [](#the-hello-world-of-unit%C2%A0testing)<font _mstmutation="1" _msthash="304343" _msttexthash="32853561">单位测试的你好世界</font>

<font _mstmutation="1" _msthash="291187" _msttexthash="58262568">注释用于将方法标记为测试。</font>```@Test```

```
public class BasicJUnit4Tests {
  @Test
  public void always_passing_test() {
    assertTrue("Always true", true);
  }
}
```

* * *

## [](#the-classlevel-and-testlevel-annotations)<font _mstmutation="1" _msthash="305903" _msttexthash="40096576">班级级和测试级注释</font>

<font _mstmutation="1" _msthash="292682" _msttexthash="53145313">注释，如**和是JUnit 4**类注释。</font>```@BeforeClass``````@AfterClass```

```
public class BasicJUnit4Tests {
  @BeforeClass
  public static void setup() {
    // Setup resource needed by all tests.
  }
  @Before
  public void beforeEveryTest() {
    // This gets executed before each test.
  }
  @Test
  public void always_passing_test() {
    assertTrue("Always true", true);
  }
  @After
  public void afterEveryTest() {
    // This gets executed after every test.
  }
  @AfterClass
  public static void cleanup() {
    // Clean up resource after all are executed.
  }
}
```

<font _mstmutation="1" _msthash="293280" _msttexthash="105994577">注释为**JUnit 5**等价物，使用以下语句导入。</font>```@BeforeAll``````@AfterAll```

```
// JUnit 5
import org.junit.jupiter.api.BeforeAll
import org.junit.jupiter.api.AfterAll
```

* * *

## [](#ignoring-a-test-vs-assumption)<font _mstmutation="1" _msthash="305267" _msttexthash="25397996">忽略测试与假设</font>

<font _mstmutation="1" _msthash="292071" _msttexthash="270967918">测试被注释忽略，或者断言可以更改为假设，JUnit 亚军将忽略失败的假设。</font>```@Ignore```

<font _mstmutation="1" _msthash="292370" _msttexthash="396055283">处理服务器与本地时区等场景时会使用假设。当假设失败时，抛出一个，JUnit跑步者将忽略它。</font>```AssumptionViolationException```

```
public class BasicJUnit4Tests {
  @Ignore("Ignored because of a good reason")
  @Test
  public void test_something() {
    assertTrue("Always fails", false);
  }
}
```

* * *

## [](#executing-tests-in%C2%A0order)<font _mstmutation="1" _msthash="307138" _msttexthash="27877681">按顺序执行测试</font>

<font _mstmutation="1" _msthash="291161" _msttexthash="152676849">一般来说，编写顺序不可知单位测试是一种好的做法。</font>

```
@FixMethodOrder(MethodSorters.NAME_ASCENDING)
public class FixedMethodOrderingTests {
  @Test
  public void first() {}
  @Test
  public void second() {}
  @Test
  public void third() {}
}
```

<font _mstmutation="1" _msthash="291759" _msttexthash="135487742">除了按测试名称的升序排序外，允许和级别排序。</font>```MethodSorter``````DEFAULT``````JVM```

* * *

## [](#adding-timeout-to%C2%A0tests)<font _mstmutation="1" _msthash="306189" _msttexthash="25804324">向测试添加超时</font>

单元测试大多具有快速执行时间：但是，在某些情况下，单位测试可能需要更长的时间。

<font _mstmutation="1" _msthash="293254" _msttexthash="69104958">在**JUnit 4**中，注释接受如下参数</font>```@Test``````timeout```

```
import org.junit.Ignore;
import org.junit.Test;
public class BasicJUnit4Tests {
  @Test(timeout = 1)
  public void timeout_test() throws InterruptedException {
    Thread.sleep(2); // Fails because it took longer than 1 second.
  }
}
```

<font _mstmutation="1" _msthash="293852" _msttexthash="83481606">在**Junit 5**中， 超时发生在断言级别</font>

```
import static java.time.Duration.ofMillis;
import static org.junit.jupiter.api.Assertions.assertTimeout;
import org.junit.jupiter.api.Test;
public class BasicJUnit5Tests {
  @Test
  public void test_timeout() {
    // Test takes 2 ms, assertion timeout in 1 ms
    assertTimeout(ofMillis(1), () -> {
      Thread.sleep(2);
    });
  }
}
```

<font _mstmutation="1" _msthash="291746" _msttexthash="205472189">有时，在所有测试中应用超时（包括和包括超时）更有意义。</font>```@BeforeEach/Before``````@AfterEach/After```

```
public class JUnitGlobalTimeoutRuleTests {
  @Rule
  public Timeout globalTimeout = new Timeout(2, TimeUnit.SECONDS);
  @Test
  public void timeout_test() throws InterruptedException {
    while(true); // Infinite loop
  }
  @Test
  public void timeout_test_pass() throws InterruptedException {
    Thread.sleep(1);
  }
}
```

* * *

## [](#using-rule-with-junit%C2%A0tests)<font _mstmutation="1" _msthash="306488" _msttexthash="35520134">使用规则与JUnit测试</font>

<font _mstmutation="1" _msthash="293241" _msttexthash="134169087">我发现在编写单元测试时很有帮助。**适用于以下规则**</font>```@Rule```

*   超时 - 上图所示
*   预期例外
*   临时折叠器
*   错误同事
*   验证

### [](#expectedexception-rule)<font _mstmutation="1" _msthash="307697" _msttexthash="19967727">预期例外规则</font>

<font _mstmutation="1" _msthash="294138" _msttexthash="291927376">此规则可用于确保测试抛出预期的异常。在**Junit 4**中， 我们可以做一些跟随的事情</font>

```
public class BasicJUnit4Tests {
  @Test(expected = NullPointerException.class)
  public void exception_test() {
    throw new IllegalArgumentException(); // Fail. Not NPE.
  }
}
```

<font _mstmutation="1" _msthash="292032" _msttexthash="136426615">然而，在**JUnit 5**中，以上可以通过以下断言实现</font>

```
public class BasicJUnit5Tests {
  @Test
  public void test_expected_exception() {
    Assertions.assertThrows(NumberFormatException.class, () -> {
      Integer.parseInt("One"); // Throws NumberFormatException
    });
  }
}
```

<font _mstmutation="1" _msthash="292630" _msttexthash="123619600">我们还可以在类级别中定义**规则**并在测试中重用</font>

```
public class JUnitRuleTests {
  @Rule
  public ExpectedException thrown = ExpectedException.none();
  @Test
  public void expectedException_inMethodLevel() {
    thrown.expect(IllegalArgumentException.class);
    thrown.expectMessage("Cause of the error");
    throw new IllegalArgumentException("Cause of the error");
  }
}
```

### [](#temporaryfolder-rule)<font _mstmutation="1" _msthash="307060" _msttexthash="18602844">临时折叠规则</font>

<font _mstmutation="1" _msthash="293527" _msttexthash="194347088">本**规则**在测试的生命周期内为创建和删除文件夹和文件夹提供便利。</font>

```
public class TemporaryFolderRuleTests {
  @Rule
  public TemporaryFolder temporaryFolder = new TemporaryFolder();
  @Test
  public void testCreatingTemporaryFileFolder() throws IOException {
    File file = temporaryFolder.newFile("testFile.txt");
    File folder = temporaryFolder.newFolder("testFolder");
    String filePath = file.getAbsolutePath();
    String folderPath = folder.getAbsolutePath();

    File testFile = new File(filePath);
    File testFolder = new File(folderPath);
    assertTrue(testFile.exists());
    assertTrue(testFolder.exists());
    assertTrue(testFolder.isDirectory());
 }
}
```

### [](#errorcollector-rule)<font _mstmutation="1" _msthash="307996" _msttexthash="20652229">错误同事规则</font>

<font _mstmutation="1" _msthash="294424" _msttexthash="429744172">在执行单元测试期间，如果有许多断言，而第一个断言失败，则随后的申报将跳过如下所示。</font>

```
@Test
public void reportFirstFailedAssertion() {
  assertTrue(false); // Failed assertion. Report. Stop execution.
  assertFalse(true); // It's never executed.
}
```

<font _mstmutation="1" _msthash="292318" _msttexthash="882298287">如果我们能得到所有失败断言的列表并立即修复它们，而不是一个接一个地修复它们，那将是有帮助的。以下是**错误合校规则**如何帮助实现这一目标。</font>

```
public class ErrorCollectorRuleTests {
  @Rule
  public ErrorCollector errorCollector = new ErrorCollector();

  @Test
  public void reportAllFailedAssertions() {
    errorCollector.checkThat(true, is(false));  // Fail. Continue
    errorCollector.checkThat(false, is(false)); // Pass. Continue
    errorCollector.checkThat(2, equalTo("a"));  // Fail. Report all
  }
}
```

还有**验证器**规则，我不会进入细节，你可以[在这里](https://zshipu.com/t?url=https://junit.org/junit4/javadoc/4.12/org/junit/rules/Verifier.html)阅读更多关于它。

<font _mstmutation="1" _msthash="293215" _msttexthash="149965140">有关两者的更多信息和区别，请参阅此[堆叠溢出](https://zshipu.com/t?url=https://stackoverflow.com/questions/41121778/junit-rule-and-classrule/41122264)帖子。</font>```@ClassRule```

* * *

## [](#junit-suites)<font _mstmutation="1" _msthash="307710" _msttexthash="11172317">JUnit套房</font>

<font _mstmutation="1" _msthash="294411" _msttexthash="183370460">JUnit 套件可用于组测试类并一起执行它们。下面是一个例子</font>

```
public class TestSuiteA {
  @Test
  public void testSuiteA() {}
}
public class TestSuiteB {
  @Test
  public void testSuiteB() {}
}
```

<font _mstmutation="1" _msthash="292305" _msttexthash="248324804">假设还有许多其他测试类，我们可以使用以下注释运行这两个或其中一个</font>

```
@RunWith(Suite.class)
@Suite.SuiteClasses({TestSuiteA.class, TestSuiteB.class})
public class TestSuite {
  // Will run tests from TestSuiteA and TestSuiteB classes
}
```

以上将导致以下

[![Alt Text](https://res.cloudinary.com/practicaldev/image/fetch/s--KXs4awOb--/c_limit%2Cf_auto%2Cfl_progressive%2Cq_auto%2Cw_880/https://thepracticaldev.s3.amazonaws.com/i/teff8b64tqfvj64nb1tj.png)](https://zshipu.com/t?url=https://res.cloudinary.com/practicaldev/image/fetch/s--KXs4awOb--/c_limit%2Cf_auto%2Cfl_progressive%2Cq_auto%2Cw_880/https://thepracticaldev.s3.amazonaws.com/i/teff8b64tqfvj64nb1tj.png)

* * *

## [](#categories-in-junit%C2%A04)<font _mstmutation="1" _msthash="307698" _msttexthash="20699341">JUnit 4 中的类别</font>

在**JUnit 4**中，我们可以利用**类别**将一组测试排除在执行之外。我们可以使用下面所示的标记界面创建尽可能多的类别

_没有实现的界面称为标记界面。_

```
public interface CategoryA {}
public interface CategoryB {}
```

<font _mstmutation="1" _msthash="304993" _msttexthash="363296089">现在，我们有两个类别，我们可以用以下所示的一个或多个类别类型对每个测试进行注释</font>

```
public class CategoriesTests {
  @Test
  public void test_categoryNone() {
    System.out.println("Test without any category");
    assert(false);
  }
  @Category(CategoryA.class)
  @Test
  public void test1() {
    System.out.println("Runs when category A is selected.");
    assert(true);
  }
  @Category(CategoryB.class)
  @Test
  public void test2() {
    System.out.println("Runs when category B is included.");
    assert(false);
  }
  @Category({CategoryA.class, CategoryB.class})
  @Test
  public void test3() {
    System.out.println("Runs when either of category is included.");
    assert(true);
  }
}
```

<font _mstmutation="1" _msthash="305617" _msttexthash="107632070">一个特殊的JUnit亚军称为用于执行这些测试</font>```Categories.class```

```
@RunWith(Categories.class)
@IncludeCategory(CategoryA.class)
@ExcludeCategory(CategoryB.class)
@SuiteClasses({CategoriesTests.class})
public class CategroyTestSuite {}
```

<font _mstmutation="1" _msthash="306241" _msttexthash="295816742">以上只会运行测试，但是，如果我们删除以下条目，然后两者兼而有之执行。</font>```test1``````test1``````test3```

```
@ExcludeCategory(CategoryB.class)
```

* * *

## [](#tagging-amp-filtering-tests-in-junit%C2%A05)<font _mstmutation="1" _msthash="321633" _msttexthash="55833011">在 JUnit 5 中标记和过滤测试</font>

<font _mstmutation="1" _msthash="307801" _msttexthash="384290413">除了**JUnit 4**中的类别外**，JUnit 5**还介绍了标记和过滤测试的能力。让我们假设我们有以下</font>

```
@Tag("development")
public class UnitTests {
  @Tag("web-layer")
  public void login_controller_test() {}
  @Tag("web-layer")
  public void logout_controller_test() {}
  @Tag("db-layer")
  @Tag("dao")
  public void user_dao_tests() {}
}
```

<font _mstmutation="1" _msthash="305604" _msttexthash="1969604">和</font>

```
@Tag("qa")
public class LoadTests {
  @Tag("auth")
  @Test
  public void login_test() {}
  @Tag("auth")
  @Test
  public void logout_test() {}
  @Tag("auth")
  @Test
  public void forgot_password_test() {}
  @Tag("report")
  @Test
  public void generate_monthly_report() {}
}
```

<font _mstmutation="1" _msthash="306228" _msttexthash="330649670">如上所示，标签适用于整个类以及单个方法。让我们执行在给定包中标记的所有测试。</font>```qa```

```
@RunWith(JUnitPlatform.class)
@SelectPackages("junit.exmaples.v2.tags")
@IncludeTags("qa")
public class JUnit5TagTests {}
```

以上将导致以下输出

[![Alt Text](https://res.cloudinary.com/practicaldev/image/fetch/s--Ja5bewub--/c_limit%2Cf_auto%2Cfl_progressive%2Cq_auto%2Cw_880/https://thepracticaldev.s3.amazonaws.com/i/ic7k31c2phuedgybahuh.png)](https://zshipu.com/t?url=https://res.cloudinary.com/practicaldev/image/fetch/s--Ja5bewub--/c_limit%2Cf_auto%2Cfl_progressive%2Cq_auto%2Cw_880/https://thepracticaldev.s3.amazonaws.com/i/ic7k31c2phuedgybahuh.png)

<font _mstmutation="1" _msthash="307476" _msttexthash="445501082">如上所示，仅运行带有标记的测试类。让我们同时运行和标记测试，但是，过滤和标记测试。</font>```qa``````qa``````development``````dao``````report```

```
@RunWith(JUnitPlatform.class)
@SelectPackages("junit.exmaples.v2.tags")
@IncludeTags({"qa", "development"})
@ExcludeTags({"report", "dao"})
public class JUnit5TagTests {}
```

<font _mstmutation="1" _msthash="308100" _msttexthash="108043949">如下所示，这两个测试注释了并排除在外。</font>```dao``````report```

[![Alt Text](https://res.cloudinary.com/practicaldev/image/fetch/s--1TghAeg_--/c_limit%2Cf_auto%2Cfl_progressive%2Cq_auto%2Cw_880/https://thepracticaldev.s3.amazonaws.com/i/gr3fdig6ikpcy1fsukca.png)](https://zshipu.com/t?url=https://res.cloudinary.com/practicaldev/image/fetch/s--1TghAeg_--/c_limit%2Cf_auto%2Cfl_progressive%2Cq_auto%2Cw_880/https://thepracticaldev.s3.amazonaws.com/i/gr3fdig6ikpcy1fsukca.png)

* * *

## [](#parametrizing-unit%C2%A0tests)<font _mstmutation="1" _msthash="320632" _msttexthash="23303020">参数化单元测试</font>

<font _mstmutation="1" _msthash="306839" _msttexthash="464128015">JUnit 允许用不同的参数执行测试，而不是用不同的参数多次复制/粘贴测试或构建自定义实用方法。</font>

```
@RunWith(Parameterized.class)
public class JUnit4ParametrizedAnnotationTests {
  @Parameter(value = 0)
  public int number;
  @Parameter(value = 1)
  public boolean expectedResult;
  // Must be static and return collection.
  @Parameters(name = "{0} is a Prime? {1}")
  public static Collection<Object[]> testData() {
    return Arrays.asList(new Object[][] {
      {1, false}, {2, true}, {7, true}, {12, false}
    });
  }
  @Test
  public void test_isPrime() {
    PrimeNumberUtil util = new PrimeNumberUtil();
    assertSame(util.isPrime(number), expectedResult);
  }
}
```

<font _mstmutation="1" _msthash="307463" _msttexthash="71903052">要使测试参数化，我们需要以下</font>```test_isPrime```

*   <font _mstmutation="1" _msthash="485459" _msttexthash="41855359">利用专业的JUnit跑步者</font>```Parametrized.class```
*   <font _mstmutation="1" _msthash="485849" _msttexthash="177739250">声明一种非私有静态方法，该方法返回带有注释的集合</font>```@Parameters```
*   <font _mstmutation="1" _msthash="486239" _msttexthash="42049410">用和值属性申报每个参数</font>```@Parameter```
*   <font _mstmutation="1" _msthash="486629" _msttexthash="42292354">使用测试中的注释字段</font>```@Parameter```

<font _mstmutation="1" _msthash="308087" _msttexthash="57018611">以下是我们参数化输出的外观</font>```test_isPrime```

[![Alt Text](https://res.cloudinary.com/practicaldev/image/fetch/s--XaV62P7z--/c_limit%2Cf_auto%2Cfl_progressive%2Cq_auto%2Cw_880/https://thepracticaldev.s3.amazonaws.com/i/dzum7w3u2n4juqdie187.png)](https://zshipu.com/t?url=https://res.cloudinary.com/practicaldev/image/fetch/s--XaV62P7z--/c_limit%2Cf_auto%2Cfl_progressive%2Cq_auto%2Cw_880/https://thepracticaldev.s3.amazonaws.com/i/dzum7w3u2n4juqdie187.png)

<font _mstmutation="1" _msthash="305890" _msttexthash="256061923">以上是使用注射，我们也可以实现相同的结果使用构造器，如下图所示。</font>```@Parameter```

```
public class JUnit4ConstructorParametrized {
  private int number;
  private boolean expectedResult;

  public JUnit4ConstructorParametrized(int input, boolean result) {
    this.number = input;
    this.expectedResult = result;
  }
  ...
}
```

<font _mstmutation="1" _msthash="306514" _msttexthash="52416455">在 JUnit 5 中，引入以下来源</font>```@ParameterizedTest```

*   <font _mstmutation="1" _msthash="484471" _msttexthash="30277">The</font> ```@ValueSource```
*   <font _mstmutation="1" _msthash="484861" _msttexthash="30277">The</font> ```@EnumSource```
*   <font _mstmutation="1" _msthash="485251" _msttexthash="30277">The</font> ```@MethodSource```
*   <font _mstmutation="1" _msthash="485641" _msttexthash="4220580">和和</font>```@CsvSource``````@CsvFileSource```

让我们详细探讨每一个。

* * *

## [](#parameterized-tests-with-a-valuesource)<font _mstmutation="1" _msthash="322244" _msttexthash="44685173">具有价值源的参数化测试</font>

<font _mstmutation="1" _msthash="308386" _msttexthash="28109744">注释允许以下声明</font>```@ValueSource```

```
@ValueSource(strings = {"Hi", "How", "Are", "You?"})
@ValueSource(ints = {10, 20, 30})
@ValueSource(longs = {1L, 2L, 3L})
@ValueSource(doubles = {1.1, 1.2, 1.3})
```

<font _mstmutation="1" _msthash="306190" _msttexthash="55562533">让我们在测试中使用上述一个</font>

```
@ParameterizedTest
@ValueSource(strings = {"Hi", "How", "Are", "You?"})
public void testStrings(String arg) {
  assertTrue(arg.length() <= 4);
}
```

## [](#parameterized-tests-with-an-enumsource)<font _mstmutation="1" _msthash="320931" _msttexthash="34403863">带内源的参数化测试</font>

<font _mstmutation="1" _msthash="307125" _msttexthash="31719207">注释可用于以下方式</font>```@EnumSource```

```
@EnumSource(Level.class)
@EnumSource(value = Level.class, names = { "MEDIUM", "HIGH"})
@EnumSource(value = Level.class, mode = Mode.INCLUDE, names = { "MEDIUM", "HIGH"})
```

<font _mstmutation="1" _msthash="307749" _msttexthash="61610653">类似，我们可以以以下方式使用</font>```ValueSource``````EnumSource```

```
@ParameterizedTest
@EnumSource(value = Level.class, mode = Mode.EXCLUDE, names = { "MEDIUM", "HIGH"})
public void testEnums_exclude_Specific(Level level) {
  assertTrue(EnumSet.of(Level.MEDIUM, Level.HIGH).contains(level));
}
```

## [](#parameterized-tests-with-a-methodsource)<font _mstmutation="1" _msthash="322556" _msttexthash="40685788">带方法源的参数化测试</font>

<font _mstmutation="1" _msthash="308685" _msttexthash="460105997">注释接受提供输入数据的方法名称。提供输入数据的方法可以返回单个参数，或者我们可以使用如下所示</font>```@MethodSource``````Arguments```

```
public class JUnit5MethodArgumentParametrizedTests {
  @ParameterizedTest
  @MethodSource("someIntegers")
  public void test_MethodSource(Integer s) {
    assertTrue(s <= 3);
  }

  static Collection<Integer> someIntegers() {
    return Arrays.asList(1,2,3);
  }
}
```

<font _mstmutation="1" _msthash="306489" _msttexthash="82394000">下面是一个例子，它也可以用来返回POJO</font>```Arguments```

```
public class JUnit5MethodArgumentParametrizedTests {
  @ParameterizedTest
  @MethodSource("argumentsSource")
  public void test_MethodSource_withMoreArgs(String month, Integer number) {
    switch(number) {
      case 1: assertEquals("Jan", month); break;
      case 2: assertEquals("Feb", month); break;
      case 3: assertEquals("Mar", month); break;
      default: assertFalse(true);
    }
  }
static Collection<Arguments> argumentsSource() {
    return Arrays.asList(
      Arguments.of("Jan", 1),
      Arguments.of("Feb", 2),
      Arguments.of("Mar", 3),
      Arguments.of("Apr", 4)); // Fail.
  }
}
```

## [](#parameterized-tests-with-a-csv%C2%A0sources)<font _mstmutation="1" _msthash="321243" _msttexthash="37229946">带 CSV 源的参数化测试</font>

当涉及到执行带有 CSV 内容的测试时**，JUnit 5**为**参数化测试**提供了两种不同类型的源

*   <font _mstmutation="1" _msthash="485420" _msttexthash="18456126">A - 逗号分离值</font>```CsvSource```
*   <font _mstmutation="1" _msthash="485810" _msttexthash="15466607">A - 引用 CSV 文件</font>```CsvFileSource```

<font _mstmutation="1" _msthash="308048" _msttexthash="22649029">下面是一个示例</font>```CsvSource```

```
@ParameterizedTest
@CsvSource(delimiter=',', value= {"1,'A'","2,'B'"})
public void test_CSVSource_commaDelimited(int i, String s) {
  assertTrue(i < 3);
  assertTrue(Arrays.asList("A", "B").contains(s));
}
```

<font _mstmutation="1" _msthash="308672" _msttexthash="52256932">假设我们有以下条目在文件下</font>```sample.csv``````src/test/resources```

```
Name, Age
Josh, 22
James, 19
Jonas, 55
```

<font _mstmutation="1" _msthash="309296" _msttexthash="23541219">案件看起来如下</font>```CsvFileSource```

```
@ParameterizedTest
@CsvFileSource(resources = "/sample.csv", numLinesToSkip = 1, delimiter = ',', encoding = "UTF-8")
public void test_CSVFileSource(String name, Integer age) {
  assertTrue(Arrays.asList("James", "Josh").contains(name));
  assertTrue(age < 50);
}
```

<font _mstmutation="1" _msthash="307099" _msttexthash="243832472">导致 2 次成功的试运行和 1 次失败，因为最后一个条目未能通过断言。</font>```sample.csv```

[![Alt Text](https://res.cloudinary.com/practicaldev/image/fetch/s--ca_IWBFE--/c_limit%2Cf_auto%2Cfl_progressive%2Cq_auto%2Cw_880/https://thepracticaldev.s3.amazonaws.com/i/x0p3khw2fmfspkj8gfqn.png)](https://zshipu.com/t?url=https://res.cloudinary.com/practicaldev/image/fetch/s--ca_IWBFE--/c_limit%2Cf_auto%2Cfl_progressive%2Cq_auto%2Cw_880/https://thepracticaldev.s3.amazonaws.com/i/x0p3khw2fmfspkj8gfqn.png)

您还可以设计自定义转换器，将CSV转换为对象。有关详细信息，请参阅[此处](https://zshipu.com/t?url=https://github.com/CodeFX-org/demo-junit-5/blob/master/src/test/java/org/codefx/demo/junit5/parameterized/CustomArgumentConverterTest.java)。

* * *

## [](#theory-in%C2%A0junit4)<font _mstmutation="1" _msthash="322855" _msttexthash="22851816">JUnit4中的理论</font>

<font _mstmutation="1" _msthash="308971" _msttexthash="507072098">注释和亚军**理论**是实验特征。与**参数化**测试相比，**理论**将数据点的所有组合都馈送至测试，如下所示。</font>```@Theory```

```
@RunWith(Theories.class)
public class JUnit4TheoriesTests {
  @DataPoint
  public static String java = "Java";
  @DataPoint
  public static String node = "node";
  @Theory
  public void test_theory(String a) {
    System.out.println(a);
  }
  @Theory
  public void test_theory_combos(String a, String b) {
    System.out.println(a + " - " + b);
  }
}
```

<font _mstmutation="1" _msthash="309595" _msttexthash="95761809">执行上述测试类时，测试将输出 2¹组合</font>```test_theory```

```
Java
node
```

<font _mstmutation="1" _msthash="307398" _msttexthash="224456713">但是，该测试将输出两个数据点的所有组合。换句话说，22个组合。</font>```test_theory_combos```

```
Java - Java
Java - node
node - Java
node - node
```

<font _mstmutation="1" _msthash="308022" _msttexthash="396992336">如果我们有以下数据点，则测试将生成 2 个*组合（2 个 args ^ 3 数据点数）。该测试将创建 33 组合。</font>```oss``````test_theory_one``````test_theory_two```

```
@DataPoints
public static String[] oss = new String[] {"Linux", "macOS", "Windows"};
@Theory
public void test_theory_one(String a, String b) {
  System.out.println(a + " - " + b);
}
@Theory
public void test_theory_two(String a, String b, String c) {
  System.out.println(a + " <-> " + b + "<->" + c);
}
```

<font _mstmutation="1" _msthash="308646" _msttexthash="33494435">以下是有效的数据点</font>

```
@DataPoints
public static Integer[] numbers() {
  return new Integer[] {1, 2, 3};
}
```

* * *

## [](#junit-5-test-displayname)<font _mstmutation="1" _msthash="324142" _msttexthash="27233206">JUnit 5 测试显示名</font>

<font _mstmutation="1" _msthash="307385" _msttexthash="260065481">JUnit 5 引入了用于给单个测试或测试类显示名称的注释，如下所示。</font>```@DisplayName```

```
@Test
@DisplayName("Test If Given Number is Prime")
public void is_prime_number_test() {}
```

它会显示如下在控制台

[![Alt Text](https://res.cloudinary.com/practicaldev/image/fetch/s--N-1ufJPD--/c_limit%2Cf_auto%2Cfl_progressive%2Cq_auto%2Cw_880/https://thepracticaldev.s3.amazonaws.com/i/tz2lf5h94q8hr1lu67y9.png)](https://zshipu.com/t?url=https://res.cloudinary.com/practicaldev/image/fetch/s--N-1ufJPD--/c_limit%2Cf_auto%2Cfl_progressive%2Cq_auto%2Cw_880/https://thepracticaldev.s3.amazonaws.com/i/tz2lf5h94q8hr1lu67y9.png)

## [](#repeating-a-junit%C2%A0test)<font _mstmutation="1" _msthash="322829" _msttexthash="21993036">重复JUnit测试</font>

<font _mstmutation="1" _msthash="308945" _msttexthash="128148956">如果需要重复单位测试 X 次数**，JUnit 5**会提供注释。</font>```@RepeatedTest```

```
@RepeatedTest(2)
public void test_executed_twice() {
  System.out.println("RepeatedTest"); // Prints twice
}
```

<font _mstmutation="1" _msthash="309569" _msttexthash="70029895">随之而来的是，变量以及对象。</font>```@RepeatedTest``````currentReptition``````totalRepetition``````TestInfo.java``````RepetitionInfo.java```

```
@RepeatedTest(value = 3, name = "{displayName} executed {currentRepetition} of {totalRepetitions}")
@DisplayName("Repeated 3 Times Test")
public void repeated_three_times(TestInfo info) {
  assertTrue("display name matches", 
     info.getDisplayName().contains("Repeated 3 Times Test"));
}
```

<font _mstmutation="1" _msthash="310193" _msttexthash="85641088">我们也可以用它来找出当前和总数重复。</font>```RepetitionInfo.java```

[![Alt Text](https://res.cloudinary.com/practicaldev/image/fetch/s--QKxatJue--/c_limit%2Cf_auto%2Cfl_progressive%2Cq_auto%2Cw_880/https://thepracticaldev.s3.amazonaws.com/i/h0u0ttdbaecb49ljg2ho.png)](https://zshipu.com/t?url=https://res.cloudinary.com/practicaldev/image/fetch/s--QKxatJue--/c_limit%2Cf_auto%2Cfl_progressive%2Cq_auto%2Cw_880/https://thepracticaldev.s3.amazonaws.com/i/h0u0ttdbaecb49ljg2ho.png)

## [](#executing-inner-class-unit-tests-using-junit-5s%C2%A0nested)<font _mstmutation="1" _msthash="322166" _msttexthash="84382766">使用 JUnit 5 嵌套执行内部类单元测试</font>

<font _mstmutation="1" _msthash="308308" _msttexthash="138492055">我很惊讶地得知，JUnit亚军不扫描内部类的测试。</font>

```
public class JUnit5NestedAnnotationTests {
  @Test
  public void test_outer_class() {
    assertTrue(true);
  }
  class JUnit5NestedAnnotationTestsNested {
    @Test
    public void test_inner_class() {
      assertFalse(true); // Never executed.
    }
  }
}
```

<font _mstmutation="1" _msthash="308932" _msttexthash="485939402">运行上述测试类时，它只会执行并报告**成功**，但是，当用注释标记内部类时，两个测试都会运行。</font>```test_outer_class``````@Nested```

[![Alt Text](https://res.cloudinary.com/practicaldev/image/fetch/s--heZkb24L--/c_limit%2Cf_auto%2Cfl_progressive%2Cq_auto%2Cw_880/https://thepracticaldev.s3.amazonaws.com/i/uzpzm8j2y3mo1kqfpluk.png)](https://zshipu.com/t?url=https://res.cloudinary.com/practicaldev/image/fetch/s--heZkb24L--/c_limit%2Cf_auto%2Cfl_progressive%2Cq_auto%2Cw_880/https://thepracticaldev.s3.amazonaws.com/i/uzpzm8j2y3mo1kqfpluk.png)

* * *

## [](#junit-5-test-lifecycle-with-testinstance-annotation)<font _mstmutation="1" _msthash="324441" _msttexthash="94631264">JUnit 5 测试生命周期与测试灌输注释</font>

<font _mstmutation="1" _msthash="310492" _msttexthash="299992615">在调用每个方法之前，JUnit 亚军创建了该类的新实例。这种行为可以在帮助下改变</font>```@Test``````@TestInstance```

```
@TestInstance(LifeCycle.PER_CLASS)
@TestInstance(LifeCycle.PER_METHOD)
```

<font _mstmutation="1" _msthash="305591" _msttexthash="61506770">有关更多信息，请查看[文档](https://zshipu.com/t?url=https://junit.org/junit5/docs/5.0.1/api/org/junit/jupiter/api/TestInstance.html)。</font>```@TestInstance(LifeCycle.PER_CLASS)```

* * *

## [](#dynamictests-using-junit-5-testfactory-annotation)<font _mstmutation="1" _msthash="320633" _msttexthash="86905143">使用 JUnit 5 测试工厂注释的动态测试</font>

<font _mstmutation="1" _msthash="306840" _msttexthash="665698228">带有注释的 JUnit 测试是静态测试，因为它们在编译时间中指定。另一方面，在运行期间生成。下面是使用该类的示例。</font>```@Test``````DynamicTests``````DynamicTests``````PrimeNumberUtil```

```
public class Junit5DynamicTests {
  @TestFactory
  Stream<DynamicTest> dynamicTests() {
    PrimeNumberUtil util = new PrimeNumberUtil();
    return IntStream.of(3, 7 , 11, 13, 15, 17)
       .mapToObj(num -> DynamicTest.dynamicTest("Is " + num + " Prime?", () -> assertTrue(util.isPrime(number))));
    }
}
```

有关动态测试的更多内容，请参阅此[博客文章](https://zshipu.com/t?url=https://blog.codefx.org/libraries/junit-5-dynamic-tests/)。

* * *

## [](#conditionally-executing-junit-5%C2%A0tests)<font _mstmutation="1" _msthash="319644" _msttexthash="35792107">有条件地执行 JUnit 5 测试</font>

<font _mstmutation="1" _msthash="305891" _msttexthash="150397858">**JUnit 5**引入了以下注释，允许有条件地执行测试。</font>

```
@EnabledOnOs, @DisabledOnOs, @EnabledOnJre, @DisabledOnJre, @EnabledForJreRange, @DisabledForJreRange, @EnabledIfSystemProperty, @EnabledIfEnvironmentVariable, @DisabledIfEnvironmentVariable, @EnableIf, @DisableIf
```

<font _mstmutation="1" _msthash="306515" _msttexthash="26548990">下面是一个使用和</font>```@EnabledOnOs``````@DisabledOnOs```

```
public class JUnit5ConditionalTests {
  @Test
  @DisabledOnOs({OS.WINDOWS, OS.OTHER})
  public void test_disabled_on_windows() {
    assertTrue(true);
  }
  @Test
  @EnabledOnOs({OS.MAC, OS.LINUX})
  public void test_enabled_on_unix() {
    assertTrue(true);
  }
  @Test
  @DisabledOnOs(OS.MAC)
  public void test_disabled_on_mac() {
    assertFalse(false);
  }
}
```

我使用的是MacBook，输出如下

[![Alt Text](https://res.cloudinary.com/practicaldev/image/fetch/s--aeXHVNm5--/c_limit%2Cf_auto%2Cfl_progressive%2Cq_auto%2Cw_880/https://thepracticaldev.s3.amazonaws.com/i/26fg5n6hhnij0scc3ot9.png)](https://zshipu.com/t?url=https://res.cloudinary.com/practicaldev/image/fetch/s--aeXHVNm5--/c_limit%2Cf_auto%2Cfl_progressive%2Cq_auto%2Cw_880/https://thepracticaldev.s3.amazonaws.com/i/26fg5n6hhnij0scc3ot9.png)

有关其他注释的示例，请查看这些[测试](https://zshipu.com/t?url=https://github.com/junit-team/junit5/blob/master/documentation/src/test/java/example/ConditionalTestExecutionDemo.java)。

* * *

