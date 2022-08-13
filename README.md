### :wave: Hi there, I'm Sadra!

<samp>

__Python__ backend developer and __Machine Learning__ enthusiast. Innovation seeker. Technical writer. Currently working on [__@collove__](https://github.com/collove) community.

</samp>
  
#### :books: My Posts

<samp>

<!-- BLOGPOSTS:START -->
 - 🚀[Connect Your Django Projects to PlanetScale Databases](https://imsadra.me/connect-your-django-projects-to-planetscale-databases) - &lt;h3 id=&quot;heading-tldr&quot;&gt;TL;DR&lt;/h3&gt;
&lt;p&gt;&lt;a target=&quot;_blank&quot; href=&quot;https://planetscale.com/&quot;&gt;PlanetScale&lt;/a&gt; is a MySQL-compatible serverless database platform. Since its database service is a bit different from the actual MySQL, there are some limitations that you can&#39;t ignore and must resolve to be able to work with their services. This post is an introduction to &lt;a target=&quot;_blank&quot; href=&quot;https://pypi.org/project/django-psdb-engine/&quot;&gt;django-psdb-engine&lt;/a&gt; package which allows you to resolve PlanteScale&#39;s limitations and connect your Django project to your PlanetScale databases with no pain.&lt;/p&gt;
&lt;h3 id=&quot;heading-what-planetscale-suggests&quot;&gt;What PlanetScale Suggests&lt;/h3&gt;
&lt;p&gt;In &lt;a target=&quot;_blank&quot; href=&quot;https://planetscale.com/docs/tutorials/connect-django-app&quot;&gt;PlanetScale documentation&lt;/a&gt;, you can see that you need to clone the PlanetScale&#39;s &lt;a target=&quot;_blank&quot; href=&quot;https://github.com/planetscale/django_psdb_engine&quot;&gt;customized database engine&lt;/a&gt; and place it into your project and use it as a self-made Django application.&lt;/p&gt;
&lt;p&gt;Long story short, I faced some issues the first time I tried connecting my Django project using the official method.&lt;/p&gt;
&lt;ul&gt;
&lt;li&gt;&lt;p&gt;If you&#39;re using Git as your main VCS, you can see some conflicts due to the duplication of both your project-level &lt;code&gt;.git&lt;/code&gt; directory and the recent cloned engine. You need to remove the &lt;code&gt;django_psdb_engine/.git&lt;/code&gt; directory first!&lt;/p&gt;
&lt;/li&gt;
&lt;li&gt;&lt;p&gt;The next issue is with &lt;code&gt;mysqlclient&lt;/code&gt; package which  django_psdb_engine requires to be able to work fine. You need to install it on your own. There might be a possibility of incompatibility between the &lt;code&gt;mysqlclient&lt;/code&gt; version you establish with the cloned engine.&lt;/p&gt;
&lt;/li&gt;
&lt;li&gt;&lt;p&gt;Finally, if you are working with tens of applications in your Django project, you may want your third-party engine to be placed somewhere like in your venv &lt;code&gt;site-packages&lt;/code&gt;, not your project&#39;s actual root path.&lt;/p&gt;
&lt;/li&gt;
&lt;/ul&gt;
&lt;p&gt;Now, let&#39;s use my method which resolves all explained issues and concerns.&lt;/p&gt;
&lt;h3 id=&quot;heading-create-account-on-planetscale&quot;&gt;Create Account on PlanetScale&lt;/h3&gt;
&lt;p&gt;&lt;em&gt;If you&#39;ve already got your PlanetScale account, skip this section.&lt;/em&gt;&lt;/p&gt;
&lt;p&gt;Create a new account or log into your account &lt;a target=&quot;_blank&quot; href=&quot;https://auth.planetscale.com/sign-in&quot;&gt;here&lt;/a&gt; and follow your way towards the dashboard.&lt;/p&gt;
&lt;p&gt;Time to create the database. Once you&#39;ve logged in, you can see the following intro which allows you to either import your existing database or create a new one.&lt;/p&gt;
&lt;p&gt;&lt;img src=&quot;https://cdn.hashnode.com/res/hashnode/image/upload/v1660396816223/zo9TgEcNu.png&quot; alt=&quot;image.png&quot; class=&quot;image--center mx-auto&quot; /&gt;&lt;/p&gt;
&lt;p&gt;Now, you need to do some setup. Choose a name for your database and select the region. Since PlanetScale stores your databases on AWS services, you can choose the region between AWS regions.&lt;/p&gt;
&lt;p&gt;&lt;img src=&quot;https://cdn.hashnode.com/res/hashnode/image/upload/v1660396956157/DSdMpz-yP.png&quot; alt=&quot;image.png&quot; class=&quot;image--center mx-auto&quot; /&gt;&lt;/p&gt;
&lt;p&gt;Once your database is initialized, click the &quot;Connect&quot; button and get your credentials.&lt;/p&gt;
&lt;p&gt;&lt;img src=&quot;https://cdn.hashnode.com/res/hashnode/image/upload/v1660397365109/Zg6PXnNbr.png&quot; alt=&quot;image.png&quot; class=&quot;image--center mx-auto&quot; /&gt;&lt;/p&gt;
&lt;p&gt;&lt;img src=&quot;https://cdn.hashnode.com/res/hashnode/image/upload/v1660397236115/Vj9oVOdSc.png&quot; alt=&quot;image.png&quot; class=&quot;image--center mx-auto&quot; /&gt;&lt;/p&gt;
&lt;p&gt;Check out both &lt;code&gt;.env&lt;/code&gt; and &lt;code&gt;settings.py&lt;/code&gt; tabs. Make sure you&#39;ve stored them in your project correctly.&lt;/p&gt;
&lt;h3 id=&quot;heading-connect-your-django-project&quot;&gt;Connect Your Django Project&lt;/h3&gt;
&lt;p&gt;Install &lt;code&gt;django-psdb-engine&lt;/code&gt; package and update the &lt;code&gt;ENGINE&lt;/code&gt; field from &lt;code&gt;settings.py&lt;/code&gt;.&lt;/p&gt;
&lt;pre&gt;&lt;code class=&quot;lang-sh&quot;&gt;$ pip install django-psdb-engine
&lt;/code&gt;&lt;/pre&gt;
&lt;p&gt;Update your &lt;code&gt;settings.py&lt;/code&gt; and change the &lt;code&gt;ENGINE&lt;/code&gt; field to apply the limitations.&lt;/p&gt;
&lt;pre&gt;&lt;code class=&quot;lang-python&quot;&gt;DATABASES = {
  &lt;span class=&quot;hljs-string&quot;&gt;&#39;default&#39;&lt;/span&gt;: {
    &lt;span class=&quot;hljs-string&quot;&gt;&#39;ENGINE&#39;&lt;/span&gt;: &lt;span class=&quot;hljs-string&quot;&gt;&#39;django_psdb_engine&#39;&lt;/span&gt;,     &lt;span class=&quot;hljs-comment&quot;&gt;# new&lt;/span&gt;
    &lt;span class=&quot;hljs-string&quot;&gt;&#39;NAME&#39;&lt;/span&gt;: os.environ.get&lpar;&lt;span class=&quot;hljs-string&quot;&gt;&#39;DB_NAME&#39;&lt;/span&gt;&rpar;,
    &lt;span class=&quot;hljs-string&quot;&gt;&#39;HOST&#39;&lt;/span&gt;: os.environ.get&lpar;&lt;span class=&quot;hljs-string&quot;&gt;&#39;DB_HOST&#39;&lt;/span&gt;&rpar;,
    &lt;span class=&quot;hljs-string&quot;&gt;&#39;PORT&#39;&lt;/span&gt;: os.environ.get&lpar;&lt;span class=&quot;hljs-string&quot;&gt;&#39;DB_PORT&#39;&lt;/span&gt;&rpar;,
    &lt;span class=&quot;hljs-string&quot;&gt;&#39;USER&#39;&lt;/span&gt;: os.environ.get&lpar;&lt;span class=&quot;hljs-string&quot;&gt;&#39;DB_USER&#39;&lt;/span&gt;&rpar;,
    &lt;span class=&quot;hljs-string&quot;&gt;&#39;PASSWORD&#39;&lt;/span&gt;: os.environ.get&lpar;&lt;span class=&quot;hljs-string&quot;&gt;&#39;DB_PASSWORD&#39;&lt;/span&gt;&rpar;,
    &lt;span class=&quot;hljs-string&quot;&gt;&#39;OPTIONS&#39;&lt;/span&gt;: {&lt;span class=&quot;hljs-string&quot;&gt;&#39;ssl&#39;&lt;/span&gt;: {&lt;span class=&quot;hljs-string&quot;&gt;&#39;ca&#39;&lt;/span&gt;: os.environ.get&lpar;&lt;span class=&quot;hljs-string&quot;&gt;&#39;MYSQL_ATTR_SSL_CA&#39;&lt;/span&gt;&rpar;}}
  }
}
&lt;/code&gt;&lt;/pre&gt;
&lt;p&gt;Since the MySQL engine uses utf8bm3 charset and its not supported by PlanetScales engine yet, you may need to add &lt;code&gt;{&#39;charset&#39;: &#39;utf8bm4&#39;}&lt;/code&gt; to &lt;code&gt;OPTIONS&lt;/code&gt; in order to migrate your changes with no problem.&lt;/p&gt;
&lt;p&gt;Finally, migrate changes and enjoy using your new database.&lt;/p&gt;
&lt;pre&gt;&lt;code class=&quot;lang-sh&quot;&gt;$ python manage.py migrate
&lt;/code&gt;&lt;/pre&gt;
&lt;h3 id=&quot;heading-final-word&quot;&gt;Final Word&lt;/h3&gt;
&lt;p&gt;Hope this quick walking-through guide helped you build your first PlanetScale database and connect your Django project to it.&lt;/p&gt;

 - 🔥[PasteMe - Paste Codes From Your Terminal](https://imsadra.me/pasteme-paste-codes-from-your-terminal) - &lt;h3 id=&quot;heading-introduction&quot;&gt;Introduction&lt;/h3&gt;
&lt;p&gt;&lt;strong&gt;PasteMe&lt;/strong&gt; is a modern open-source RESTful pastebin service that allows users to paste their source codes, snippets, and code blocks right from their command-line interfaces and terminals!&lt;/p&gt;
&lt;blockquote&gt;
&lt;p&gt;Legends claimed that this project is developed from space! So let&#39;s find out.&lt;/p&gt;
&lt;/blockquote&gt;
&lt;ul&gt;
&lt;li&gt;&lt;a target=&quot;_blank&quot; href=&quot;https://pasteme.pythonanywhere.com&quot;&gt;Check out PasteMe; deployed on PythonAnywhere services&lt;/a&gt;!&lt;/li&gt;
&lt;/ul&gt;
&lt;p&gt;&lt;img src=&quot;https://cdn.hashnode.com/res/hashnode/image/upload/v1659101718796/5V_KdPj0V.png&quot; alt=&quot;Artboard 1.png&quot; class=&quot;image--center mx-auto&quot; /&gt;&lt;/p&gt;
&lt;h4 id=&quot;heading-the-point-where-all-things-began&quot;&gt;The point where all things began..&lt;/h4&gt;
&lt;p&gt;I personally was familiar with &lt;a target=&quot;_blank&quot; href=&quot;https://en.wikipedia.org/wiki/Pastebin&quot;&gt;pastebin&lt;/a&gt; services. Since I&#39;m so into those black and dark interfaces and CLIs, I needed a piece of software that enables me to share my programming bugs, issues, or even gold code pieces with others in the community. I found some packages but I was looking for something fancier with more options until Hashnode announced an extraordinary Hackathon partnering with &lt;a target=&quot;_blank&quot; href=&quot;https://planetscale.com/&quot;&gt;PlanetScale&lt;/a&gt; and that made me open a new fresh terminal tab immediately and run &lt;code&gt;$ git init&lt;/code&gt; and start developing my idea named &quot;PasteMe&quot;!&lt;/p&gt;
&lt;h4 id=&quot;heading-paste-me-up-there&quot;&gt;Paste me up there..&lt;/h4&gt;
&lt;p&gt;As developers, we are always developing a system full of architectures, components, and dependencies. It&#39;s so common we run into issues and problems during worktime. There&#39;s been a lot of times when I was stuck in making a function work perfectly but the key to that perfectness was in another configuration file from another module in a package. That being said, sometimes after hours of boring work time and struggling with fixing my bugs, my buggy source codes were whispering to me like &quot;&lt;em&gt;Paste me Sadra..please.. do it.. Paste me up there..&lt;/em&gt;&quot; which brings us to PasteMe!&lt;/p&gt;
&lt;h3 id=&quot;heading-1-features&quot;&gt;1. Features&lt;/h3&gt;
&lt;p&gt;There is a well-structured RESTful service behind PasteMe which allows users to paste their snippets and code blocks to the powerful PlanetScale databases by using &lt;code&gt;pasteme-cli&lt;/code&gt; package. The endpoints are designed responsively, meaning all developers from other platforms can build their own tools and interact with PasteMe&#39;s APIs in their products.&lt;/p&gt;
&lt;h4 id=&quot;heading-11-pasteme-webservice&quot;&gt;1.1. PasteMe webservice&lt;/h4&gt;
&lt;ul&gt;
&lt;li&gt;Dynamic section showing the PyPI package statistics and GitHub repos&#39; stars.&lt;/li&gt;
&lt;li&gt;Showing the pasted source codes in popular light and dark themes + line number.&lt;/li&gt;
&lt;li&gt;An &lt;a target=&quot;_blank&quot; href=&quot;https://asciinema.org/&quot;&gt;asciinema&lt;/a&gt; cast player showing the setup process and how you can start using PasteMe.&lt;/li&gt;
&lt;li&gt;A perfect auto-generated API documentation for developers.&lt;/li&gt;
&lt;li&gt;A minimal weblog.&lt;/li&gt;
&lt;/ul&gt;
&lt;h4 id=&quot;heading-12-pasteme-cli-python-package-sdk&quot;&gt;1.2. &lt;code&gt;pasteme-cli&lt;/code&gt; Python package &lpar;SDK&rpar;&lt;/h4&gt;
&lt;ul&gt;
&lt;li&gt;Available for Windows and Linux distributions.&lt;/li&gt;
&lt;li&gt;Minimum dependency.&lt;/li&gt;
&lt;li&gt;Easy to set up and use.&lt;/li&gt;
&lt;li&gt;Accessible from your CLIs and within your Python projects as a package.&lt;/li&gt;
&lt;/ul&gt;
&lt;h3 id=&quot;heading-2-start-pasting&quot;&gt;2. Start Pasting&lt;/h3&gt;
&lt;p&gt;In order to use PasteMe, simply install the &lt;code&gt;pasteme-cli&lt;/code&gt; package via either &lt;a target=&quot;_blank&quot; href=&quot;https://pip.pypa.io/en/stable/installation/&quot;&gt;pip package manager&lt;/a&gt; or by building the package source and dive through the codes.&lt;/p&gt;
&lt;p&gt;Run the following command and make this package available on your machine.&lt;/p&gt;
&lt;pre&gt;&lt;code class=&quot;lang-sh&quot;&gt;$ pip install pasteme-cli
...
$ pasteme --&lt;span class=&quot;hljs-built_in&quot;&gt;help&lt;/span&gt;
&lt;/code&gt;&lt;/pre&gt;
&lt;div class=&quot;hn-table&quot;&gt;
&lt;table&gt;
&lt;thead&gt;
&lt;tr&gt;
&lt;td&gt;&lt;strong&gt;Option&lt;/strong&gt;&lt;/td&gt;&lt;td&gt;&lt;strong&gt;Long&lt;/strong&gt;&lt;/td&gt;&lt;td&gt;&lt;strong&gt;Default&lt;/strong&gt;&lt;/td&gt;&lt;td&gt;&lt;strong&gt;Description&lt;/strong&gt;&lt;/td&gt;&lt;/tr&gt;
&lt;/thead&gt;
&lt;tbody&gt;
&lt;tr&gt;
&lt;td&gt;&lt;strong&gt;-t&lt;/strong&gt;&lt;/td&gt;&lt;td&gt;--title&lt;/td&gt;&lt;td&gt;&quot;Untitled&quot;&lt;/td&gt;&lt;td&gt;Paste Title&lt;/td&gt;&lt;/tr&gt;
&lt;tr&gt;
&lt;td&gt;&lt;strong&gt;-l&lt;/strong&gt;&lt;/td&gt;&lt;td&gt;--language&lt;/td&gt;&lt;td&gt;PlainText&lt;/td&gt;&lt;td&gt;Source code language for highlighting&lt;/td&gt;&lt;/tr&gt;
&lt;tr&gt;
&lt;td&gt;&lt;strong&gt;-T&lt;/strong&gt;&lt;/td&gt;&lt;td&gt;--theme&lt;/td&gt;&lt;td&gt;Default Light&lt;/td&gt;&lt;td&gt;Paste theme&lt;/td&gt;&lt;/tr&gt;
&lt;tr&gt;
&lt;td&gt;&lt;strong&gt;-s&lt;/strong&gt;&lt;/td&gt;&lt;td&gt;--start&lt;/td&gt;&lt;td&gt;first line&lt;/td&gt;&lt;td&gt;Source code starting line&lt;/td&gt;&lt;/tr&gt;
&lt;tr&gt;
&lt;td&gt;&lt;strong&gt;-e&lt;/strong&gt;&lt;/td&gt;&lt;td&gt;--end&lt;/td&gt;&lt;td&gt;last line&lt;/td&gt;&lt;td&gt;Source code ending line&lt;/td&gt;&lt;/tr&gt;
&lt;tr&gt;
&lt;td&gt;&lt;strong&gt;-v&lt;/strong&gt;&lt;/td&gt;&lt;td&gt;--verbose&lt;/td&gt;&lt;td&gt;False&lt;/td&gt;&lt;td&gt;More details&lt;/td&gt;&lt;/tr&gt;
&lt;tr&gt;
&lt;td&gt;&lt;strong&gt;-h&lt;/strong&gt;&lt;/td&gt;&lt;td&gt;--help&lt;/td&gt;&lt;td&gt;-&lt;/td&gt;&lt;td&gt;Help command&lt;/td&gt;&lt;/tr&gt;
&lt;/tbody&gt;
&lt;/table&gt;
&lt;/div&gt;&lt;p&gt;Imagine I have a Python function in my &lt;code&gt;program.py&lt;/code&gt; that doesn&#39;t print out the greetings message for some reason. Let&#39;s paste it and share it.&lt;/p&gt;
&lt;pre&gt;&lt;code class=&quot;lang-python&quot;&gt;&lt;span class=&quot;hljs-function&quot;&gt;&lt;span class=&quot;hljs-keyword&quot;&gt;def&lt;/span&gt; &lt;span class=&quot;hljs-title&quot;&gt;hello_world&lt;/span&gt;&lpar;&lt;span class=&quot;hljs-params&quot;&gt;name&lt;/span&gt;&rpar;:&lt;/span&gt;
    &lt;span class=&quot;hljs-keyword&quot;&gt;return&lt;/span&gt; &lt;span class=&quot;hljs-string&quot;&gt;f&#39;Hello &lt;span class=&quot;hljs-subst&quot;&gt;{name}&lt;/span&gt;. How are you today?!&#39;&lt;/span&gt;

&lt;span class=&quot;hljs-keyword&quot;&gt;if&lt;/span&gt; __name__ == &lt;span class=&quot;hljs-string&quot;&gt;&#39;__main__&#39;&lt;/span&gt;:
    name = input&lpar;&lt;span class=&quot;hljs-string&quot;&gt;&#39;Your name: &#39;&lt;/span&gt;&rpar;
    hello_world&lpar;name&rpar;
&lt;/code&gt;&lt;/pre&gt;
&lt;p&gt;I open a new terminal/cmd tab. Since I&#39;m an Atom &lpar;A popular text editor&rpar; fan, I want to paste it with the &lt;code&gt;atom one dark&lt;/code&gt; theme.&lt;/p&gt;
&lt;pre&gt;&lt;code class=&quot;lang-shell&quot;&gt;$ pasteme -t &quot;My hello_world&lpar;&rpar; doesn&#39;t show the message!!&quot; -l python -T atom-one-dark program.py
PASTE --&amp;gt; https://pasteme.pythonanywhere.com/paste/2425b
$
&lt;/code&gt;&lt;/pre&gt;
&lt;p&gt;Right after running that command, I can see the URL to my paste. Let&#39;s browse it.&lt;/p&gt;
&lt;p&gt;&lt;img src=&quot;https://cdn.hashnode.com/res/hashnode/image/upload/v1658493956883/K_9PlVXPC.png&quot; alt=&quot;image.png&quot; class=&quot;image--center mx-auto&quot; /&gt;&lt;/p&gt;
&lt;p&gt;And volla!&lt;/p&gt;
&lt;p&gt;Now, I want to paste everything inside the &lt;code&gt;if&lt;/code&gt; statement only. I simply use &lt;code&gt;-s&lt;/code&gt; &lpar;or &lt;code&gt;--start&lt;/code&gt;&rpar; for this purpose. &lpar;Use &lt;code&gt;-e&lt;/code&gt; to specify the ending line&rpar;&lt;/p&gt;
&lt;pre&gt;&lt;code class=&quot;lang-shell&quot;&gt;$ pasteme ... -s 5 program.py
&lt;/code&gt;&lt;/pre&gt;
&lt;p&gt;&lt;img src=&quot;https://cdn.hashnode.com/res/hashnode/image/upload/v1658505548560/WEW649DA_.png&quot; alt=&quot;image &lpar;3&rpar;.png&quot; class=&quot;image--center mx-auto&quot; /&gt;&lt;/p&gt;
&lt;h3 id=&quot;heading-3-language-andamp-theme-support&quot;&gt;3. Language &amp;amp; Theme Support&lt;/h3&gt;
&lt;p&gt;PasteMe supports various programming and markup languages for highlighting at the moment. You can paste your source codes in different popular themes as well!&lt;/p&gt;
&lt;h4 id=&quot;heading-31-supported-languages&quot;&gt;3.1. Supported languages&lt;/h4&gt;
&lt;ul&gt;
&lt;li&gt;Bash &lpar;e.g. &lt;code&gt;-l bash script.sh&lt;/code&gt;&rpar;&lt;/li&gt;
&lt;li&gt;C &lpar;e.g. &lt;code&gt;-l c program.c&lt;/code&gt;&rpar;&lt;/li&gt;
&lt;li&gt;C++ &lpar;e.g. &lt;code&gt;-l cpp program.cpp&lt;/code&gt;&rpar;&lt;/li&gt;
&lt;li&gt;C# &lpar;e.g. &lt;code&gt;-l csharp program.cpp&lt;/code&gt;&rpar;&lt;/li&gt;
&lt;li&gt;CSS &lpar;e.g. &lt;code&gt;-l css styles.css&lt;/code&gt;&rpar;&lt;/li&gt;
&lt;li&gt;Go &lpar;e.g. &lt;code&gt;-l go service.go&lt;/code&gt;&rpar;&lt;/li&gt;
&lt;li&gt;HTML &lpar;e.g. &lt;code&gt;-l html index.html&lt;/code&gt;&rpar;&lt;/li&gt;
&lt;li&gt;Java &lpar;e.g. &lt;code&gt;-l java program.java&lt;/code&gt;&rpar;&lt;/li&gt;
&lt;li&gt;JavaScript &lpar;e.g. &lt;code&gt;-l js script.js&lt;/code&gt;&rpar;&lt;/li&gt;
&lt;li&gt;JSON &lpar;e.g. &lt;code&gt;-l json data.json&lt;/code&gt;&rpar;&lt;/li&gt;
&lt;li&gt;Lua &lpar;e.g. &lt;code&gt;-l lua program.lua&lt;/code&gt;&rpar;&lt;/li&gt;
&lt;li&gt;MarkDown &lpar;e.g. &lt;code&gt;-l md README.md&lt;/code&gt;&rpar;&lt;/li&gt;
&lt;li&gt;PHP &lpar;e.g. &lt;code&gt;-l php login.php&lt;/code&gt;&rpar;&lt;/li&gt;
&lt;li&gt;PlainText &lpar;e.g. &lt;code&gt;file.txt&lt;/code&gt; - no options needed&rpar;&lt;/li&gt;
&lt;li&gt;Python &lpar;e.g. &lt;code&gt;-l python setup.py&lt;/code&gt;&rpar;&lt;/li&gt;
&lt;li&gt;Ruby &lpar;e.g. &lt;code&gt;-l rb program.rb&lt;/code&gt;&rpar;&lt;/li&gt;
&lt;/ul&gt;
&lt;h4 id=&quot;heading-32-supported-themes&quot;&gt;3.2. Supported themes&lt;/h4&gt;
&lt;ul&gt;
&lt;li&gt;Default Light Theme &lpar;e.g. &lt;code&gt;file.type&lt;/code&gt; - no options needed&rpar;&lt;/li&gt;
&lt;li&gt;Default Dark Theme &lpar;e.g. &lt;code&gt;-T dark file.type&lt;/code&gt;&rpar;&lt;/li&gt;
&lt;li&gt;Github Light Theme &lpar;e.g. &lt;code&gt;-T github file.type&lt;/code&gt;&rpar;&lt;/li&gt;
&lt;li&gt;Github Dark Theme &lpar;e.g. &lt;code&gt;-T github-dark file.type&lt;/code&gt;&rpar;&lt;/li&gt;
&lt;li&gt;Atom One Light Theme &lpar;e.g. &lt;code&gt;-T atom-one-light file.type&lt;/code&gt;&rpar;&lt;/li&gt;
&lt;li&gt;Atom One Dark Theme &lpar;e.g. &lt;code&gt;-T atom-one-dark file.type&lt;/code&gt;&rpar;&lt;/li&gt;
&lt;/ul&gt;
&lt;iframe src=&quot;https://www.linkedin.com/embed/feed/update/urn:li:ugcPost:6956301808440860673&quot; height=&quot;530&quot; width=&quot;100%&quot;&gt;&lt;/iframe&gt;

&lt;h3 id=&quot;heading-4-pypi-andamp-github-integrations&quot;&gt;4. PyPI &amp;amp; GitHub Integrations&lt;/h3&gt;
&lt;p&gt;The &lt;strong&gt;Py&lt;/strong&gt;thon &lt;strong&gt;P&lt;/strong&gt;ackage &lt;strong&gt;I&lt;/strong&gt;ndex, abbreviated as &lt;a target=&quot;_blank&quot; href=&quot;https://pypi.org/&quot;&gt;PyPI&lt;/a&gt;, is the official third-party software repository for Python. This is where &lt;code&gt;pasteme-cli&lt;/code&gt; is archived as well. By checking the &lt;a target=&quot;_blank&quot; href=&quot;https://pasteme.pythonanywhere.com&quot;&gt;home page of PasteMe&lt;/a&gt;, you&#39;ll notice the following section.&lt;/p&gt;
&lt;p&gt;&lt;img src=&quot;https://cdn.hashnode.com/res/hashnode/image/upload/v1658497433854/gRLtBx3Qp.png&quot; alt=&quot;image &lpar;2&rpar;.png&quot; class=&quot;image--center mx-auto&quot; /&gt;&lt;/p&gt;
&lt;p&gt;There is a model called &lt;code&gt;Statistic&lt;/code&gt; in &lt;code&gt;pypi&lt;/code&gt; application of the project which is responsible for storing all statistics gathered from api.github.com and https://pypistats.org/api. Therefore, I designed a scheduled task that runs a &lt;a target=&quot;_blank&quot; href=&quot;https://docs.djangoproject.com/en/4.0/howto/custom-management-commands/&quot;&gt;custom command&lt;/a&gt; every day at a specific time and that command actually updates the &lt;code&gt;Statistic&lt;/code&gt; model by creating a new record to the table based on the information responded from the endpoints.&lt;/p&gt;
&lt;h3 id=&quot;heading-5-technologies-used-in-pasteme&quot;&gt;5. Technologies Used in PasteMe&lt;/h3&gt;
&lt;p&gt;In this section, we&#39;re going to talk about the tools and frameworks that I used to build up PasteMe.&lt;/p&gt;
&lt;h4 id=&quot;heading-51-frameworks-andamp-tools&quot;&gt;5.1. Frameworks &amp;amp; Tools&lt;/h4&gt;
&lt;ul&gt;
&lt;li&gt;Django Framework &lpar;Python back-end framework&rpar; + DRF&lt;/li&gt;
&lt;li&gt;Bootstrap Framework &lpar;Integrated with Django&#39;s template engine&rpar;&lt;/li&gt;
&lt;li&gt;&lt;a target=&quot;_blank&quot; href=&quot;https://github.com/ionelmc/cookiecutter-pylibrary&quot;&gt;Pylibrary Cookiecutter&lt;/a&gt; &lpar;to develop the &lt;code&gt;pasteme-cli&lt;/code&gt; Python package&rpar;&lt;/li&gt;
&lt;/ul&gt;
&lt;h4 id=&quot;heading-52-infrastructures&quot;&gt;5.2. Infrastructures&lt;/h4&gt;
&lt;ul&gt;
&lt;li&gt;Deployed on &lt;a target=&quot;_blank&quot; href=&quot;https://pythonanywhere.com&quot;&gt;PythonAnywhere&lt;/a&gt; &lpar;&lt;a target=&quot;_blank&quot; href=&quot;https://pasteme.pythonanywhere.com&quot;&gt;Check out PasteMe Live!&lt;/a&gt;&rpar;&lt;/li&gt;
&lt;li&gt;Database is powered by &lt;a target=&quot;_blank&quot; href=&quot;https://planetscale.com&quot;&gt;PlanetScale&lt;/a&gt;&lt;/li&gt;
&lt;/ul&gt;
&lt;h3 id=&quot;heading-development&quot;&gt;Development&lt;/h3&gt;
&lt;p&gt;Both the package and web service have tests that make the development process way easier with a lower risk of failure. Keep up with the README/CONTRIBUTING docs and make your way towards the contribution.&lt;/p&gt;
&lt;p&gt;&lt;a target=&quot;_blank&quot; href=&quot;https://github.com/collove/pasteme#service-installation&quot;&gt;Check out PasteMe&#39;s readme&lt;/a&gt; document for a complete local installation guide. You can also connect your locally cloned PasteMe to a PlanetScale FREE database by following the guide as well.&lt;/p&gt;
&lt;h3 id=&quot;heading-useful-links&quot;&gt;Useful Links&lt;/h3&gt;
&lt;ul&gt;
&lt;li&gt;&lt;a target=&quot;_blank&quot; href=&quot;https://pasteme.pythonanywhere.com&quot;&gt;Check out PasteMe LIVE&lt;/a&gt;.&lt;/li&gt;
&lt;li&gt;&lt;a target=&quot;_blank&quot; href=&quot;https://github.com/collove/pasteme&quot;&gt;Web service repository on Github&lt;/a&gt;.&lt;/li&gt;
&lt;li&gt;&lt;a target=&quot;_blank&quot; href=&quot;https://github.com/collove/pasteme-cli&quot;&gt;Python package repository on Github&lt;/a&gt;.&lt;/li&gt;
&lt;li&gt;&lt;a target=&quot;_blank&quot; href=&quot;https://pypi.org/project/pasteme-cli&quot;&gt;Python package on PyPI&lt;/a&gt;.&lt;/li&gt;
&lt;/ul&gt;
&lt;h3 id=&quot;heading-thanks&quot;&gt;Thanks&lt;/h3&gt;
&lt;p&gt;I&#39;m truly glad about the partnership between Hashnode and PlanetScale that made this awesome &lt;a target=&quot;_blank&quot; href=&quot;https://townhall.hashnode.com/planetscale-hackathon&quot;&gt;July&#39;s Hackathon&lt;/a&gt;! Thanks for your awesome services and support. 🌹&lt;/p&gt;
&lt;h3 id=&quot;heading-socials&quot;&gt;Socials&lt;/h3&gt;
&lt;iframe src=&quot;https://www.linkedin.com/embed/feed/update/urn:li:share:6956291231597346817&quot; height=&quot;811&quot; width=&quot;100%&quot;&gt;&lt;/iframe&gt;
 - 💯[Become an Open Source Contributor](https://imsadra.me/become-an-open-source-contributor) - &lt;p&gt;We have used many open-source tools and software in our career life and technical journey so far but how are they being developed? How do people make an effort to do open source and make use of them? How can we be part of an open-source community?&lt;/p&gt;
&lt;p&gt;In this article, we&#39;ll talk about some concepts behind the Open Source world. The way you should start your open source journey as a developer and professional ethics in an open-source community. If you&#39;re interested in open-source collaboration and you want to be a better open-source maintainer, this is a good point to start.&lt;/p&gt;
&lt;blockquote&gt;
&lt;p&gt;You may not find this article that technical, but I tried my best to share my thoughts and experiences since I started working on open-source projects on the GitHub platform.&lt;/p&gt;
&lt;/blockquote&gt;
&lt;p&gt;I assume you are already familiar with some basic development tools and platforms and you are about to work on your favorite repositories.&lt;/p&gt;
&lt;h3 id=&quot;heading-1-how-to-start-the-journey&quot;&gt;1. How to Start the Journey&lt;/h3&gt;
&lt;p&gt;In this section, we are going to talk about some tips before you start contributing to the Open Source.&lt;/p&gt;
&lt;ul&gt;
&lt;li&gt;&lt;p&gt;&lt;strong&gt;Be humble and sociable&lt;/strong&gt;. An open-source community is where members from all across the world are grouped together to help each other and make awesome solutions for the problems existing in the real world. Everyone is contributing with love. Many of them are not paid to contribute. Being kind and affable in open source communities is the most positive ethical habit. Since you may not be familiar with other regions&#39; cultures, so always be kind and respectful.&lt;/p&gt;
&lt;/li&gt;
&lt;li&gt;&lt;p&gt;&lt;strong&gt;Always start small&lt;/strong&gt;. That&#39;s how you improve. When you start from small projects, you won&#39;t be stuck at much complexity and the development path and issues are much more sensible compared to the bigger tools.&lt;/p&gt;
&lt;/li&gt;
&lt;li&gt;&lt;p&gt;&lt;strong&gt;Find the active projects&lt;/strong&gt;. As a contributor, you are happy with a project that has active maintainers and communities so your changes will be reviewed quickly and your questions will be answered faster. You can choose whatever project you find cool for contribution. Make sure they are not abandoned and they do accept contributions. Check out the &lt;code&gt;README&lt;/code&gt; and/or the &lt;code&gt;CONTRIBUTING&lt;/code&gt; file in the repository. You may look for the projects that your product relies on or even you may contribute to more popular projects to make a better resume and career experience.&lt;/p&gt;
&lt;/li&gt;
&lt;li&gt;&lt;p&gt;&lt;strong&gt;Contribution is not just contributing to the actual code&lt;/strong&gt;. Many tools have their documentation in different languages. The documentation section is where most new contributors start their contributions from. You can find typo issues or even start translating the entire document into another language for example. Since many projects don&#39;t care about test developments sometimes, writing their tests is another good way to start.&lt;/p&gt;
&lt;/li&gt;
&lt;li&gt;&lt;p&gt;&lt;strong&gt;Using an open-source tool may make you a contributor&lt;/strong&gt;. You may work with an open-source tool/framework. You see that the tool you are using is showing some unusual errors and there is something wrong with the tool. You check its repository and you find the issue. You decide to work on it and fix that bug. That&#39;s counted as a contribution as well.&lt;/p&gt;
&lt;/li&gt;
&lt;li&gt;&lt;p&gt;&lt;strong&gt;Start from the issues&lt;/strong&gt;. You can simply fix an issue that another member faced a while ago. You don&#39;t need to experience it yourself to be able to fix the issue. Most repositories use GitHub&#39;s issue tab. That&#39;s a good section for starting. Make sure you keep your conversation public. Your decisions may help other developers/users one day.&lt;/p&gt;
&lt;/li&gt;
&lt;li&gt;&lt;p&gt;&lt;strong&gt;Make friends out of the open-source&lt;/strong&gt;. One of the coolest parts of open-source is when you can contact other people from other countries and make connections. Making new friends in the open-source world allows you to grow up faster. Join communities, forums, and conferences, and try reaching out to others.&lt;/p&gt;
&lt;/li&gt;
&lt;li&gt;&lt;p&gt;&lt;strong&gt;No room for panicking&lt;/strong&gt;! If your reasonable feature request gets rejected by a maintainer, or it&#39;s been months since you opened a PR and no one has reviewed it yet &lpar;a dead/abandoned repository&rpar;, don&#39;t get disappointed. If your PR gets closed, there is a reason for that. With all respect, ask for the reason and remember that in your further contributions. They want to grow the project as you do that&#39;s why I suggest you open an issue first and talk about the improvements you think would be perfect and once they agreed, you can start the development. You&#39;ll save more time for sure.&lt;/p&gt;
&lt;/li&gt;
&lt;/ul&gt;
&lt;h3 id=&quot;heading-2-contributing-to-large-scale-projects&quot;&gt;2. Contributing to Large-Scale Projects&lt;/h3&gt;
&lt;p&gt;You may be wondering about contributions to larger popular repositories. As we understood, you always better start from smaller-scale projects first. You can figure out the contribution phases much easier since there is less complexity in those types of projects.&lt;/p&gt;
&lt;p&gt;You can find the following files and directories in your desired repository. Let&#39;s see what they are for and how you can use them.&lt;/p&gt;
&lt;ul&gt;
&lt;li&gt;&lt;strong&gt;Git-based components&lt;/strong&gt;&lt;ul&gt;
&lt;li&gt;&lt;code&gt;.git&lt;/code&gt; - The actual git initiated folder used in the project.&lt;/li&gt;
&lt;li&gt;&lt;code&gt;.gitignore&lt;/code&gt; - Contains ignored patterns that git doesn&#39;t care of.&lt;/li&gt;
&lt;li&gt;&lt;code&gt;.gitattributes&lt;/code&gt; - To set attributes for files.&lt;/li&gt;
&lt;/ul&gt;
&lt;/li&gt;
&lt;li&gt;&lt;strong&gt;GitHub-based components&lt;/strong&gt;&lt;ul&gt;
&lt;li&gt;&lt;code&gt;.github&lt;/code&gt; - A directory where GitHub looks for action workflows, templates, and etc documents in.&lt;/li&gt;
&lt;li&gt;&lt;code&gt;README&lt;/code&gt; - It might be an &lt;code&gt;rst&lt;/code&gt;, &lt;code&gt;txt&lt;/code&gt;, or &lt;code&gt;md&lt;/code&gt; file that contains explanations about an app or the repository.&lt;/li&gt;
&lt;li&gt;&lt;code&gt;LICENSE&lt;/code&gt; - A document that the repository is licensed under.&lt;/li&gt;
&lt;li&gt;&lt;code&gt;CONTRIBUTING&lt;/code&gt; - Contains the contribution steps you need to know about the repository.&lt;/li&gt;
&lt;/ul&gt;
&lt;/li&gt;
&lt;/ul&gt;
&lt;p&gt;The first step is to always check the &lt;code&gt;README&lt;/code&gt; file first. Make sure the repository is active and then navigate to the &quot;Contribution&quot; section or the &lt;code&gt;CONTRIBUTING&lt;/code&gt; file. Here is a &lt;code&gt;CONTRIBUTING&lt;/code&gt; file sample depicted.&lt;/p&gt;
&lt;p&gt;&lt;img src=&quot;https://cdn.hashnode.com/res/hashnode/image/upload/v1655550421367/LaUW65Tgg.png&quot; alt=&quot;image.png&quot; class=&quot;image--center mx-auto&quot; /&gt;&lt;/p&gt;
&lt;p&gt;To contribute to larger-scale projects, you should know the project first. Read its official documentation and &lt;a target=&quot;_blank&quot; href=&quot;https://en.wikipedia.org/wiki/Docstring&quot;&gt;docstrings&lt;/a&gt; to understand each part. Dive through the project&#39;s files and directories. Understand its structure and architecture whether it could be monolithic or microservice. Whether it&#39;s Procedural or OOP.&lt;/p&gt;
&lt;p&gt;Larger projects are separated into different applications and modules so the development will be much easier for the contributors. If you want to improve a function, you find both the module and tests much easier. A good practice could be reading the project&#39;s tests so you can find what kind of role each part do in the project.&lt;/p&gt;
&lt;p&gt;In larger projects such as programming languages, there would be a guideline called &quot;Developer Guideline&quot; for those who are planning to contribute to the project. For example, &lt;a target=&quot;_blank&quot; href=&quot;https://devguide.python.org/&quot;&gt;Python has its own development guideline&lt;/a&gt; and there is everything described there.&lt;/p&gt;
&lt;p&gt;The tips we reviewed earlier would help you to become a better Open Source contributor. However, in most cases, you might be the maintainer of a project. In terms of maintenance, this road might be a bit challenging but in the following topics, we&#39;ll talk about some maintenance tips that make you a better open-source manager.&lt;/p&gt;
&lt;h3 id=&quot;heading-3-jack-of-all-trades-master-of-something&quot;&gt;3. Jack of All Trades, Master of &lt;em&gt;Something&lt;/em&gt;&lt;/h3&gt;
&lt;p&gt;As an open-source maintainer, sometimes you are in a circumstance where you need to start everything on your own. You need logos, banners, perfect documentation, and a clean well-structured repository and you are the only one standing. Having experience in some different out-of-circle skills may survive you in that situation. I personally believe that an open-source maintainer should be familiar with all technical fields. However, he/she must be an expert in a specific field. That&#39;s how you can give birth to a new idea and make it ready to fly. A little bit of marketing skill is always handy.&lt;/p&gt;
&lt;p&gt;You should not only be highly skilled in your technical field to build a perfect foundation, but you better know about side skills as well. At least be able to satisfy your project&#39;s requirements.&lt;/p&gt;
&lt;blockquote&gt;
&lt;p&gt;Open Source leadership requires significant technical skills in open source and the audacity in boldly using them  but only after youve studied the lay of the land, understood the group dynamics, and done some of the dirty work yourself. &lpar;The Linux Foundation&rpar;&lt;/p&gt;
&lt;/blockquote&gt;
&lt;h3 id=&quot;heading-4-why-making-it-open-source&quot;&gt;4. Why Making it Open-Source&lt;/h3&gt;
&lt;p&gt;We are living in a world full of problems and difficulties. As a software developer, you are here to solve problems using your skills. No matter whether it&#39;s open-source or closed. Each project you work on is actually nothing but an idea. Let me explain with an example.&lt;/p&gt;
&lt;p&gt;Consider you have an operating system installed on your computer. You&#39;ve installed an application that you want once your system boots up, that application gets executed as well. You write a Python script to do that thing and it&#39;s working now. You have solved your problem. You can keep the script and use it whenever you face this issue again. You will no longer need to solve this issue again since you have a reusable solution for it. That script is nothing but plain text. The idea behind that is the most important thing.&lt;/p&gt;
&lt;p&gt;When you make your script open-source, you are actually making that idea publically available to others. There are tons of benefits to open-source development. Maybe the most important one is that you figure out whether your idea/solution has the potential to improve.&lt;/p&gt;
&lt;p&gt;Most of today&#39;s popular repositories were only an idea one day that was published publically and now they have many contributors and collaborators. The companies that are using those open-source projects are their awesome supporters.&lt;/p&gt;
&lt;h3 id=&quot;heading-5-licensing&quot;&gt;5. Licensing&lt;/h3&gt;
&lt;p&gt;An open-source product is something that is licensed under an open-source license. When your project has no license, it doesn&#39;t mean that your project is open-source. Since licensing is a crucial part, I suggest you choose them carefully. If you don&#39;t feel comfortable with the existing &lt;a target=&quot;_blank&quot; href=&quot;https://choosealicense.com/licenses/&quot;&gt;open-source licenses&lt;/a&gt; and you think they might not fit with your work, you can design your own license which I don&#39;t recommend.&lt;/p&gt;
&lt;h3 id=&quot;heading-6-no-one-cares-about-my-projects&quot;&gt;6. No One Cares About my Projects&lt;/h3&gt;
&lt;p&gt;Many developers find it a bit tough to host their projects on platforms like Github and develop them in open source. Not technically but basically. You might have asked the following questions so I got my answers for you.&lt;/p&gt;
&lt;h4 id=&quot;heading-61-my-code-is-not-that-clean-and-perfect-to-push-to-github&quot;&gt;6.1. My code is not that clean and perfect to push to GitHub!&lt;/h4&gt;
&lt;p&gt;There is no necessity for your project to be AWESOME to be able to be hosted on a platform like GitHub. You push the idea to make its implementation perfect. The idea you are working on might be a solution for another popular repository issue.&lt;/p&gt;
&lt;h4 id=&quot;heading-62-no-one-reaches-my-projects-and-it-has-only-a-few-stars&quot;&gt;6.2. No one reaches my projects and it has only a few stars!&lt;/h4&gt;
&lt;p&gt;You don&#39;t need to compare your new idea to those that have hundreds of contributors and stars. Keep making it better. Ask for help. Make issues on your own project. Join communities and ask them about your idea. Let them give you perspectives. Find out whether your idea has the potential to grow or not.&lt;/p&gt;
&lt;p&gt;These are the most concerns that I myself faced many times in my journey whenever I wanted to start an open-source project. Please let me know if you have any questions about this journey in the comments. :&rpar;&lt;/p&gt;
&lt;h3 id=&quot;heading-conclusion&quot;&gt;Conclusion&lt;/h3&gt;
&lt;p&gt;In this article, we talked about the crucial tips that you can use in your open-source journey to have a better experience and enjoy working on different projects even the popular ones. We also explained the licensing phase and at the end, we took a quick look and open-source maintenance.&lt;/p&gt;

 - 🚀[Unit Testing in Python &amp; Best Practices](https://imsadra.me/unit-testing-in-python-and-best-practices) - &lt;p&gt;In this article, I&#39;ll help you to understand the basics of unit testing in Python and then, we&#39;ll talk about the awesome practices that make your tests way more understandable and maintainable. If you are looking for a point to start writing tests for your Python projects, here we are. Without further ado, let&#39;s see some magic.&lt;/p&gt;
&lt;h3 id=&quot;heading-1-software-testing-andamp-unit-tests&quot;&gt;1. Software Testing &amp;amp; Unit Tests&lt;/h3&gt;
&lt;p&gt;Software testing is a stage where we test our project to make sure it raises the proper exceptions, returns the expected values, evaluates the entities properly, and so on. We can test our project in different ways. That&#39;s why we have multiple testing solutions. One of those solutions is called Unit Testing.&lt;/p&gt;
&lt;p&gt;In a car, we have multiple electrical control units. We have the radio unit, lights, battery, battery charger, different systematic modules, etc. Whenever you face an issue in the electric system, you can simply check each unit to find the issue. This approach is more useful when your units are related to each other like when the radio needs the power coming from the battery. When the radio is not working as expected, you need to check both the battery unit and the radio one to find the issue. Imagine there was a software that was testing every single unit of your car and preparing you a report out of the tests! I would buy that.&lt;/p&gt;
&lt;p&gt;We know what units are like for now. Every project is made up of different units. The integrity between these units makes an integration system that has its own testing solution called Integration Testing. Let&#39;s get back to the units and testing itself.&lt;/p&gt;
&lt;h3 id=&quot;heading-2-why-testing&quot;&gt;2. Why Testing&lt;/h3&gt;
&lt;p&gt;Many developers are struggling when it comes to writing tests like your project might still work well without having any tests, but is it still easy to maintain? Do other developers enjoy working on your project? Do new contributors pass the onboarding phase so quickly?&lt;/p&gt;
&lt;ul&gt;
&lt;li&gt;&lt;p&gt;&lt;strong&gt;Increase the coverage and maintainability&lt;/strong&gt;. Most projects are being judged by their coverage status. Higher code coverage, happier developers.&lt;/p&gt;
&lt;/li&gt;
&lt;li&gt;&lt;p&gt;&lt;strong&gt;With tests, fix bugs before implementing&lt;/strong&gt;. In Test-driven Development, developers try to design tests before they get their hands dirty with the actual implementation. They test a feature before they even add it to the project. Once it passed the tests statistically and logically, they merge it.&lt;/p&gt;
&lt;/li&gt;
&lt;li&gt;&lt;p&gt;&lt;strong&gt;Tests are like documents&lt;/strong&gt;. With clean tests, you&#39;ll increase the maintainability of your project and the new developers can easily understand the different parts of the project by reading the tests and finding each part&#39;s requirements. When someone reads the tests, he understands what that unit is supposed to do. That&#39;s where Guido Van Rossum says:&lt;/p&gt;
&lt;/li&gt;
&lt;/ul&gt;
&lt;blockquote&gt;
&lt;p&gt;Code is read more often than it is written.&lt;/p&gt;
&lt;/blockquote&gt;
&lt;h3 id=&quot;heading-3-isolate-your-tests&quot;&gt;3. Isolate Your Tests&lt;/h3&gt;
&lt;p&gt;When it comes to isolation in Python, it reminds me of virtual environments there. They are actually the same but in fact, we have them in case of writing unit tests. So what is an isolated test?&lt;/p&gt;
&lt;p&gt;Each test you write should be kept and run isolated which means, none of your tests should affect any other part of your project or any other tests living in the same file or project. Your tests are not supposed to change the real things such as data in the databases. That&#39;s the actual meaning of isolation where your tests only do their jobs and delete all their footsteps. Your tests should not depend on any other test.&lt;/p&gt;
&lt;p&gt;Isolation makes your tests much easier to read. We are always afraid of dependent stuff and finding the issues in such a situation is so painful. An isolated test shows that any failure that we are having in the result will be solved in that specific test block and nowhere else. When you are running the entire project&#39;s tests and you have a failure on test number two, with isolated tests, it means that you can solve the issue in that test function and there is no chance for test number two to depend on any other test.&lt;/p&gt;
&lt;h3 id=&quot;heading-4-lets-do-some-code&quot;&gt;4. Let&#39;s Do Some Code&lt;/h3&gt;
&lt;p&gt;Enough talking. In Python, we have different powerful testing tools. The one we are using today is the &lt;a target=&quot;_blank&quot; href=&quot;https://docs.python.org/3/library/unittest.html&quot;&gt;unittest&lt;/a&gt; standard library which provides different features without installing any additional library or package. You can use &lt;a target=&quot;_blank&quot; href=&quot;https://docs.pytest.org/&quot;&gt;PyTest&lt;/a&gt; as well. Simply open a &lt;code&gt;tests.py&lt;/code&gt; file and import the requirements.&lt;/p&gt;
&lt;pre&gt;&lt;code class=&quot;lang-python&quot;&gt;&lt;span class=&quot;hljs-keyword&quot;&gt;import&lt;/span&gt; unittest
&lt;span class=&quot;hljs-keyword&quot;&gt;from&lt;/span&gt; math &lt;span class=&quot;hljs-keyword&quot;&gt;import&lt;/span&gt; sqrt, power, pi
&lt;/code&gt;&lt;/pre&gt;
&lt;p&gt;Notice we&#39;ve imported some math functions as well. In the following simple test case, we are testing these functions from the math standard library to check if it still gives us the right answer.&lt;/p&gt;
&lt;pre&gt;&lt;code class=&quot;lang-python&quot;&gt;&lt;span class=&quot;hljs-class&quot;&gt;&lt;span class=&quot;hljs-keyword&quot;&gt;class&lt;/span&gt; &lt;span class=&quot;hljs-title&quot;&gt;TestMathLib&lt;/span&gt;&lpar;&lt;span class=&quot;hljs-params&quot;&gt;unittest.TestCase&lt;/span&gt;&rpar;:&lt;/span&gt;

    &lt;span class=&quot;hljs-function&quot;&gt;&lt;span class=&quot;hljs-keyword&quot;&gt;def&lt;/span&gt; &lt;span class=&quot;hljs-title&quot;&gt;test_if_sqrt_still_works&lt;/span&gt;&lpar;&lt;span class=&quot;hljs-params&quot;&gt;self&lt;/span&gt;&rpar;:&lt;/span&gt;
        self.assertEqual&lpar;sqrt&lpar;&lt;span class=&quot;hljs-number&quot;&gt;25&lt;/span&gt;&rpar;, &lt;span class=&quot;hljs-number&quot;&gt;5&lt;/span&gt;&rpar;

    &lt;span class=&quot;hljs-function&quot;&gt;&lt;span class=&quot;hljs-keyword&quot;&gt;def&lt;/span&gt; &lt;span class=&quot;hljs-title&quot;&gt;to_test_if_pi_still_starts_with_three&lt;/span&gt;&lpar;&lt;span class=&quot;hljs-params&quot;&gt;self&lt;/span&gt;&rpar;:&lt;/span&gt;
        self.assertEqual&lpar;pi // &lt;span class=&quot;hljs-number&quot;&gt;1&lt;/span&gt;, &lt;span class=&quot;hljs-number&quot;&gt;3&lt;/span&gt;&rpar;

    &lt;span class=&quot;hljs-function&quot;&gt;&lt;span class=&quot;hljs-keyword&quot;&gt;def&lt;/span&gt; &lt;span class=&quot;hljs-title&quot;&gt;test_if_power_still_works&lt;/span&gt;&lpar;&lt;span class=&quot;hljs-params&quot;&gt;self&lt;/span&gt;&rpar;:&lt;/span&gt;
        self.assertEqual&lpar;pow&lpar;&lt;span class=&quot;hljs-number&quot;&gt;2&lt;/span&gt;, &lt;span class=&quot;hljs-number&quot;&gt;3&lt;/span&gt;&rpar;, &lt;span class=&quot;hljs-number&quot;&gt;8&lt;/span&gt;&rpar;
&lt;/code&gt;&lt;/pre&gt;
&lt;p&gt;We got three tests so far. Let&#39;s run them. At the end of the file, to make it executable from the shell, we add the following line.&lt;/p&gt;
&lt;pre&gt;&lt;code class=&quot;lang-python&quot;&gt;&lt;span class=&quot;hljs-keyword&quot;&gt;if&lt;/span&gt; __name__ == &lt;span class=&quot;hljs-string&quot;&gt;&#39;__main__&#39;&lt;/span&gt;: unittest.main&lpar;&rpar;
&lt;/code&gt;&lt;/pre&gt;
&lt;p&gt;Using the &lt;code&gt;python&lt;/code&gt; command for running our tests is not recommended at all. What if you need to run a specific app&#39;s tests?! Then Python can not help anymore. Simply use the &lt;code&gt;unittest&lt;/code&gt; command-line tool for more options and stability.&lt;/p&gt;
&lt;p&gt;Now, open a fresh terminal tab and change your directory and run the following command.&lt;/p&gt;
&lt;pre&gt;&lt;code class=&quot;lang-shell&quot;&gt;python -m unittest
&lt;/code&gt;&lt;/pre&gt;
&lt;p&gt;Here is the result.&lt;/p&gt;
&lt;pre&gt;&lt;code class=&quot;lang-shell&quot;&gt;..
----------------------------------------------------------------------
Ran 2 tests in 0.010s

OK
&lt;/code&gt;&lt;/pre&gt;
&lt;p&gt;It looks like we got something! Since running the &lt;code&gt;unittest&lt;/code&gt; command with no flags runs all tests, why did it run only two of them? What are those two dots up there?!&lt;/p&gt;
&lt;p&gt;The &lt;code&gt;unittest&lt;/code&gt; library just runs the test functions that are starting with the word &lt;code&gt;test&lt;/code&gt; which means, in that test, our &lt;code&gt;pi&lt;/code&gt; test is missing. To make it visible, add the keyword &lt;code&gt;test&lt;/code&gt; at the beginning of the method name.&lt;/p&gt;
&lt;pre&gt;&lt;code class=&quot;lang-shell&quot;&gt;...
----------------------------------------------------------------------
Ran 3 tests in 0.010s

OK
&lt;/code&gt;&lt;/pre&gt;
&lt;p&gt;Those characters at the beginning of the result show the status of each test execution. It shows that it found three tests and all those tests are passed. There will be &lt;code&gt;F&lt;/code&gt; per each test failure other than a dot. There is another situation where you might get &lt;code&gt;E&lt;/code&gt;. It means that there is a problem with your test itself like there might be a syntax error or typo issue inside your test.&lt;/p&gt;
&lt;h3 id=&quot;heading-5-damp-andamp-dry-principles-in-your-tests&quot;&gt;5. DAMP &amp;amp; DRY Principles in Your Tests&lt;/h3&gt;
&lt;p&gt;These two famous principles allow you to write clean and easy-to-understand tests. In this part, we&#39;ll talk about the beautiful names you can choose for your test cases and we&#39;ll be using the &lt;code&gt;setUp&lpar;&rpar;&lt;/code&gt; method to improve our tests.&lt;/p&gt;
&lt;h4 id=&quot;heading-51-descriptive-and-meaningful-phrases-damp&quot;&gt;5.1. Descriptive and Meaningful Phrases &lpar;DAMP&rpar;&lt;/h4&gt;
&lt;p&gt;As we understood earlier, the &lt;code&gt;unittest&lt;/code&gt; library will not run those tests starting with any word other than &lt;code&gt;test&lt;/code&gt;. It&#39;s also a good reason to change the name of our function to a longer phrase like &lt;code&gt;test_if_multiplication_works&lt;/code&gt; or &lt;code&gt;test_user_validation&lt;/code&gt;. A name that represents what that test does. Also, make sure your test class is starting with the word &lt;code&gt;Test&lt;/code&gt; because as your testing system grows, you may need some mocking classes which are not supposed to be tested independently and that&#39;s how you separate your testing functions.&lt;/p&gt;
&lt;h4 id=&quot;heading-52-dont-repeat-yourself-dry&quot;&gt;5.2. Don&#39;t Repeat Yourself &lpar;DRY&rpar;&lt;/h4&gt;
&lt;p&gt;Consider we need an object from a class called &lt;code&gt;Car&lt;/code&gt; to test some of its methods and actions.&lt;/p&gt;
&lt;pre&gt;&lt;code class=&quot;lang-python&quot;&gt;&lt;span class=&quot;hljs-class&quot;&gt;&lt;span class=&quot;hljs-keyword&quot;&gt;class&lt;/span&gt; &lt;span class=&quot;hljs-title&quot;&gt;TestCar&lt;/span&gt;&lpar;&lt;span class=&quot;hljs-params&quot;&gt;unittest.TestCase&lt;/span&gt;&rpar;:&lt;/span&gt;

    &lt;span class=&quot;hljs-function&quot;&gt;&lt;span class=&quot;hljs-keyword&quot;&gt;def&lt;/span&gt; &lt;span class=&quot;hljs-title&quot;&gt;test_if_car_can_move_forward&lt;/span&gt;&lpar;&lt;span class=&quot;hljs-params&quot;&gt;self&lt;/span&gt;&rpar;:&lt;/span&gt;
        my_car = Car&lpar;&rpar;
        self.assertEqual&lpar;my_car.move&lpar;&lt;span class=&quot;hljs-string&quot;&gt;&#39;forward&#39;&lt;/span&gt;&rpar;, &lt;span class=&quot;hljs-string&quot;&gt;&#39;car is moving forward&#39;&lt;/span&gt;&rpar;

    &lt;span class=&quot;hljs-function&quot;&gt;&lt;span class=&quot;hljs-keyword&quot;&gt;def&lt;/span&gt; &lt;span class=&quot;hljs-title&quot;&gt;test_if_car_can_move_backward&lt;/span&gt;&lpar;&lt;span class=&quot;hljs-params&quot;&gt;self&lt;/span&gt;&rpar;:&lt;/span&gt;
        my_car = Car&lpar;&rpar;
        self.assertEqual&lpar;my_car.move&lpar;&lt;span class=&quot;hljs-string&quot;&gt;&#39;backward&#39;&lt;/span&gt;&rpar;, &lt;span class=&quot;hljs-string&quot;&gt;&#39;car is moving backward&#39;&lt;/span&gt;&rpar;
    ...
&lt;/code&gt;&lt;/pre&gt;
&lt;p&gt;Notice we are recreating an object from the Car class over and over. Use the &lt;code&gt;setUp&lpar;&rpar;&lt;/code&gt; method to define whatever you need per test. This method is called before each test you have.&lt;/p&gt;
&lt;pre&gt;&lt;code class=&quot;lang-python&quot;&gt;&lt;span class=&quot;hljs-class&quot;&gt;&lt;span class=&quot;hljs-keyword&quot;&gt;class&lt;/span&gt; &lt;span class=&quot;hljs-title&quot;&gt;TestCar&lt;/span&gt;&lpar;&lt;span class=&quot;hljs-params&quot;&gt;unittest.TestCase&lt;/span&gt;&rpar;:&lt;/span&gt;

    &lt;span class=&quot;hljs-function&quot;&gt;&lt;span class=&quot;hljs-keyword&quot;&gt;def&lt;/span&gt; &lt;span class=&quot;hljs-title&quot;&gt;setUp&lt;/span&gt;&lpar;&lt;span class=&quot;hljs-params&quot;&gt;self&lt;/span&gt;&rpar;:&lt;/span&gt;
      self.my_car= Car&lpar;&rpar;

    &lt;span class=&quot;hljs-function&quot;&gt;&lt;span class=&quot;hljs-keyword&quot;&gt;def&lt;/span&gt; &lt;span class=&quot;hljs-title&quot;&gt;test_if_car_can_move_forward&lt;/span&gt;&lpar;&lt;span class=&quot;hljs-params&quot;&gt;self&lt;/span&gt;&rpar;:&lt;/span&gt;
        self.assertEqual&lpar;self.my_car.move&lpar;&lt;span class=&quot;hljs-string&quot;&gt;&#39;forward&#39;&lt;/span&gt;&rpar;, &lt;span class=&quot;hljs-string&quot;&gt;&#39;car is moving forward&#39;&lt;/span&gt;&rpar;

    &lt;span class=&quot;hljs-function&quot;&gt;&lt;span class=&quot;hljs-keyword&quot;&gt;def&lt;/span&gt; &lt;span class=&quot;hljs-title&quot;&gt;test_if_car_can_move_backward&lt;/span&gt;&lpar;&lt;span class=&quot;hljs-params&quot;&gt;self&lt;/span&gt;&rpar;:&lt;/span&gt;
        self.assertEqual&lpar;self.my_car.move&lpar;&lt;span class=&quot;hljs-string&quot;&gt;&#39;backward&#39;&lt;/span&gt;&rpar;, &lt;span class=&quot;hljs-string&quot;&gt;&#39;car is moving backward&#39;&lt;/span&gt;&rpar;
    ...
&lt;/code&gt;&lt;/pre&gt;
&lt;p&gt;That&#39;s how you observe the DRY principle with &lt;code&gt;setUp&lpar;&rpar;&lt;/code&gt; method in your tests. For more information about these methods, check out &lt;a target=&quot;_blank&quot; href=&quot;https://imsadra.me/setup-and-teardown-in-python-unit-testing&quot;&gt;setUp&lpar;&rpar; &amp;amp; tearDown&lpar;&rpar; in Python Unit Testing&lt;/a&gt;.&lt;/p&gt;
&lt;h3 id=&quot;heading-6-mocks&quot;&gt;6. Mocks&lt;/h3&gt;
&lt;p&gt;Mocking is not a test solution. It&#39;s actually part of some testing systems. Some projects may have mocks, some may not. With mocks, you can simulate some necessities that your test may need in order to test a feature of the project.&lt;/p&gt;
&lt;p&gt;As an example, imagine you have a function in your project that makes an HTTP request to an API and serializes the returned data. Now, you want to test the serialization phase by writing unit tests. What if that server crashes at the time you run your test? Your test will fail for sure but there is no room for blaming your project&#39;s feature right? It was not its fault. It was the server&#39;s crash that made your test fail.&lt;/p&gt;
&lt;p&gt;&lt;img src=&quot;https://cdn.hashnode.com/res/hashnode/image/upload/v1654197885475/tal8PxkE_.png&quot; alt=&quot;Artboard 1@4x.png&quot; class=&quot;image--center mx-auto&quot; /&gt;&lt;/p&gt;
&lt;p&gt;Mocking is the art of simulation. You can create a function that acts as the API server and you use it in the body of your test block. Then, your test failures will appear whenever there is something wrong with your project, not others&#39;.&lt;/p&gt;
&lt;p&gt;In the following example, we are mocking the &lt;code&gt;requests.get&lpar;&rpar;&lt;/code&gt; action. We have a module called &lt;code&gt;discovery.py&lt;/code&gt; that contains the following function.&lt;/p&gt;
&lt;pre&gt;&lt;code class=&quot;lang-python&quot;&gt;&lt;span class=&quot;hljs-keyword&quot;&gt;from&lt;/span&gt; requests &lt;span class=&quot;hljs-keyword&quot;&gt;import&lt;/span&gt; get

&lt;span class=&quot;hljs-function&quot;&gt;&lt;span class=&quot;hljs-keyword&quot;&gt;def&lt;/span&gt; &lt;span class=&quot;hljs-title&quot;&gt;get_data&lt;/span&gt;&lpar;&lt;span class=&quot;hljs-params&quot;&gt;link, index&lt;/span&gt;&rpar;:&lt;/span&gt;
    response = get&lpar;&lt;span class=&quot;hljs-string&quot;&gt;f&#39;&lt;span class=&quot;hljs-subst&quot;&gt;{link}&lt;/span&gt;/&lt;span class=&quot;hljs-subst&quot;&gt;{index}&lt;/span&gt;&#39;&lt;/span&gt;&rpar;
    &lt;span class=&quot;hljs-keyword&quot;&gt;return&lt;/span&gt; response
&lt;/code&gt;&lt;/pre&gt;
&lt;p&gt;In our &lt;code&gt;tests.py&lt;/code&gt;, we need to test the &lt;code&gt;get_data&lpar;&rpar;&lt;/code&gt; function. Normally, my test will fail when the &lt;code&gt;link&lt;/code&gt; is not reachable and the server might be the issue. This is how we mock that functionality.&lt;/p&gt;
&lt;pre&gt;&lt;code class=&quot;lang-python&quot;&gt;&lt;span class=&quot;hljs-keyword&quot;&gt;from&lt;/span&gt; unittest &lt;span class=&quot;hljs-keyword&quot;&gt;import&lt;/span&gt; TestCase, main, mock

&lt;span class=&quot;hljs-keyword&quot;&gt;from&lt;/span&gt; discovery &lt;span class=&quot;hljs-keyword&quot;&gt;import&lt;/span&gt; get_data
&lt;span class=&quot;hljs-keyword&quot;&gt;from&lt;/span&gt; requests &lt;span class=&quot;hljs-keyword&quot;&gt;import&lt;/span&gt; Response

succeed_response = Response&lpar;&rpar;
succeed_response.status_code = &lt;span class=&quot;hljs-number&quot;&gt;200&lt;/span&gt;

failed_response = Response&lpar;&rpar;
failed_response.status_code = &lt;span class=&quot;hljs-number&quot;&gt;404&lt;/span&gt;

&lt;span class=&quot;hljs-class&quot;&gt;&lt;span class=&quot;hljs-keyword&quot;&gt;class&lt;/span&gt; &lt;span class=&quot;hljs-title&quot;&gt;DiscoveryTest&lt;/span&gt;&lpar;&lt;span class=&quot;hljs-params&quot;&gt;TestCase&lt;/span&gt;&rpar;:&lt;/span&gt;

&lt;span class=&quot;hljs-meta&quot;&gt;    @mock.patch&lpar;&#39;discovery.get&#39;, return_value=succeed_response&rpar;&lt;/span&gt;
    &lt;span class=&quot;hljs-function&quot;&gt;&lt;span class=&quot;hljs-keyword&quot;&gt;def&lt;/span&gt; &lt;span class=&quot;hljs-title&quot;&gt;test_with_valid_index&lt;/span&gt;&lpar;&lt;span class=&quot;hljs-params&quot;&gt;self, mock_obj&lt;/span&gt;&rpar;:&lt;/span&gt;
        response = get_data&lpar;&lt;span class=&quot;hljs-string&quot;&gt;&#39;https://google.com&#39;&lt;/span&gt;, &lt;span class=&quot;hljs-string&quot;&gt;&#39;search&#39;&lt;/span&gt;&rpar;
        self.assertEqual&lpar;response.status_code, &lt;span class=&quot;hljs-number&quot;&gt;200&lt;/span&gt;&rpar;

&lt;span class=&quot;hljs-meta&quot;&gt;    @mock.patch&lpar;&#39;discovery.get&#39;, return_value=failed_response&rpar;&lt;/span&gt;
    &lt;span class=&quot;hljs-function&quot;&gt;&lt;span class=&quot;hljs-keyword&quot;&gt;def&lt;/span&gt; &lt;span class=&quot;hljs-title&quot;&gt;test_with_invalid_index&lt;/span&gt;&lpar;&lt;span class=&quot;hljs-params&quot;&gt;self, moch_obj&lt;/span&gt;&rpar;:&lt;/span&gt;
        response = get_data&lpar;&lt;span class=&quot;hljs-string&quot;&gt;&#39;https://google.com&#39;&lt;/span&gt;, &lt;span class=&quot;hljs-string&quot;&gt;&#39;somewhere&#39;&lt;/span&gt;&rpar;
        self.assertEqual&lpar;response.status_code, &lt;span class=&quot;hljs-number&quot;&gt;404&lt;/span&gt;&rpar;

&lt;span class=&quot;hljs-keyword&quot;&gt;if&lt;/span&gt; __name__ == &lt;span class=&quot;hljs-string&quot;&gt;&#39;__main__&#39;&lt;/span&gt;: main&lpar;&rpar;
&lt;/code&gt;&lt;/pre&gt;
&lt;p&gt;At first, this implementation might look a bit confusing. We are basically mocking the &lt;code&gt;get&lpar;&rpar;&lt;/code&gt; entity from the &lt;code&gt;discovery&lt;/code&gt; module as you can see in the patch decorators then, we specify the return value that we expect for the test.&lt;/p&gt;
&lt;p&gt;In the &lt;code&gt;unittest&lt;/code&gt; package, you can use mocks in different ways. You can implement them as decorators, context managers, or even purely in the &lt;code&gt;setUp&lt;/code&gt; and &lt;code&gt;tearDown&lt;/code&gt; methods. I prefer using decorators as it&#39;s more readable in my opinion.&lt;/p&gt;
&lt;h3 id=&quot;heading-7-best-practices&quot;&gt;7. Best Practices&lt;/h3&gt;
&lt;p&gt;We have pretty much talked about the major topics. In this section, we are going to take a look at the awesome practices that you can observe to upgrade your tests and give them a better look.&lt;/p&gt;
&lt;ul&gt;
&lt;li&gt;&lt;p&gt;&lt;strong&gt;Make your tests so fast in executing&lt;/strong&gt;. Developers expect plug-and-play and fast tests. Imagine an open-source contributor who aims to improve a feature from your project. He does not care about your test development. All he wants is to make his changes and test them and fix any incoming bugs. If the testing process takes too long to execute, he might regret testing his changes in future collaborations.&lt;/p&gt;
&lt;/li&gt;
&lt;li&gt;&lt;p&gt;&lt;strong&gt;Design your tests readable and simple&lt;/strong&gt;. Always think of someone who will read your test and make improvements based on what he has learned from your tests. Your tests might be much more valuable than your documentation for your developers because they are trained to learn technically.&lt;/p&gt;
&lt;/li&gt;
&lt;li&gt;&lt;p&gt;&lt;strong&gt;Observe DRY and DAMP principles in your tests&lt;/strong&gt;. Having these methods in mind would help you to design better tests. A good test contains proper naming, simplicity, isolation, and maintainability.&lt;/p&gt;
&lt;/li&gt;
&lt;li&gt;&lt;p&gt;&lt;strong&gt;Have a convention for storing your project&#39;s tests&lt;/strong&gt;. In Python, the best practice for storing your test files is to have a package called &lt;code&gt;tests&lt;/code&gt; and keep your tests there. Make sure your test files&#39; names start with &lt;code&gt;test_&lt;/code&gt; which allows test runners to find your tests immediately. The &lt;code&gt;unittest&lt;/code&gt; package has a discovery feature that always looks for the &lt;code&gt;test&lt;/code&gt; keyword by default. A brilliant structure is as follows.&lt;/p&gt;
&lt;/li&gt;
&lt;/ul&gt;
&lt;pre&gt;&lt;code class=&quot;lang-shell&quot;&gt;project
 accounting
 transaction
 management
 tests
    __init__.py
    test_accounting.py
    test_management.py
    test_transaction.py
 README.md
 app.py
&lt;/code&gt;&lt;/pre&gt;
&lt;ul&gt;
&lt;li&gt;&lt;strong&gt;Make your tests cross-platform&lt;/strong&gt;. Having a cross-platform test comes in handy when it&#39;s about CI/CD development where the automated systems work with your tests. Having a stable structure for storing your tests is a crucial key. Simplifying, you have a nice structure when you can filter the test execution with a few options or commands.&lt;/li&gt;
&lt;/ul&gt;
&lt;h3 id=&quot;heading-conclusion&quot;&gt;Conclusion&lt;/h3&gt;
&lt;p&gt;We reached the end but testing never ends. Having a good testing platform would definitely save a lot of your team&#39;s time. We saw a simple introduction to Python unit testing at first and then talked about some best practices and principles that would improve your testing skills for sure.&lt;/p&gt;

 - 🔥[Dependency Hell](https://imsadra.me/dependency-hell) - &lt;p&gt;This is where things get a scary turn! In this article, we are going to talk about a real concern that many maintainers and developers from the past decades were worried about. This topic does not rely on any specific framework, programming language, etc. Since our products need some requirements in order to work efficiently and we &lpar;developers&rpar; hate to waste our time on nothing, we need to think about this BIG issue.&lt;/p&gt;
&lt;p&gt;We all know that our projects whether it&#39;s a mobile application software or a Python program that interacts with an API, need some necessities to be working fine. Those necessities are called &quot;Dependencies&quot; in our world.&lt;/p&gt;
&lt;p&gt;I&#39;m pretty sure that you&#39;ve already been in some situations where you needed to install some packages in order to be able to work with some functionalities and implementations. Most of the time, you simply use a package manager and install your required packages. Each installed package may need some other modules and packages to provide you the facilities and so on.&lt;/p&gt;
&lt;p&gt;Now, imagine your project getting bigger and bigger. As it grows and you add new features, it requires more dependencies and modules. We can shape the dependencies into a graph-like illustration that shows the actual application dependencies and the required packages by dependencies.&lt;/p&gt;
&lt;p&gt;For this article, we use &lt;code&gt;PKG NAME:version&lt;/code&gt; pattern to show the package name and the version number. We also use those routing lines to show the package dependency as well. In the following image, you can see that our &lt;code&gt;App&lt;/code&gt; has some dependencies on &lt;code&gt;Q:3&lt;/code&gt;, &lt;code&gt;Z:5&lt;/code&gt;, &lt;code&gt;F:1&lt;/code&gt;, and &lt;code&gt;S:4&lt;/code&gt; packages. Some of those dependencies have their own requirements on &lt;code&gt;E:8&lt;/code&gt;, &lt;code&gt;P:1&lt;/code&gt;, and &lt;code&gt;H:2&lt;/code&gt; and that&#39;s how it goes.&lt;/p&gt;
&lt;p&gt;&lt;img src=&quot;https://cdn.hashnode.com/res/hashnode/image/upload/v1653670363347/XOm_cpwAe.png&quot; alt=&quot;Artboard 1@4x.png&quot; /&gt;&lt;/p&gt;
&lt;p&gt;Let&#39;s see how things get messy!&lt;/p&gt;
&lt;h3 id=&quot;heading-many-dependencies-situation&quot;&gt;Many Dependencies Situation&lt;/h3&gt;
&lt;p&gt;You&#39;ve probably seen this situation where your product has lots of dependencies on the different live/dead packages. I&#39;m using live and dead words to show a package state. A dead package refers to a package that&#39;s totally abandoned and no one contributes to it anymore. Don&#39;t want to make a sad story out of this article so let&#39;s move on. :&rpar;&lt;/p&gt;
&lt;p&gt;Overall, having tens of dependencies might bring you some troubles especially when you&#39;re planning for an urgent update. You&#39;ve been working on a project for two years and now, you have tens of features in your project. You need to upgrade your main framework in order to fix some security bugs or even better performance. You are using &lt;code&gt;PKG A:1&lt;/code&gt; and now, after two years of maintenance, you update the main framework so then your &lt;code&gt;PKG A:1&lt;/code&gt; can&#39;t keep up with the new version of the framework anymore since it was released two years earlier. This is a common issue in the case of installing packages as 3rd party applications. That would be a huge mess.&lt;/p&gt;
&lt;p&gt;The best approach is to implement things you need on your own as you can do. Like the &lt;strong&gt;minimal&lt;/strong&gt; features and implementations that you may need in the different parts of your product. Why would you use a third-party package for getting the current system time since you can use the same functionality from the make-ready available local site-packages? &lpar;Also known as the standard libraries as well&rpar;&lt;/p&gt;
&lt;p&gt;At the end of the article, we will talk about the solutions and best conventions.&lt;/p&gt;
&lt;h3 id=&quot;heading-chain-of-dependencies-situation&quot;&gt;Chain of Dependencies Situation&lt;/h3&gt;
&lt;p&gt;In this situation, your project has a dependency on &lt;code&gt;PKG A:1&lt;/code&gt; which depends on &lt;code&gt;PKG B:1&lt;/code&gt; which depends on &lt;code&gt;PKG C:1&lt;/code&gt; which depends on &lt;code&gt;PKG D:1&lt;/code&gt;, and so on. This is a horrific situation where you have a chain of dependency behind your project. Whenever a piece of this chain breaks, your project won&#39;t work as usual. At least, some features may not respond correctly.&lt;/p&gt;
&lt;p&gt;One of the common issues that maintainers run into in the case of having such a chain is when you have a conflict with the versions of packages in a system. Remember that you can not have multiple versions of the same package installed on a computer normally. For example, we are not able to keep both &lt;code&gt;PKG C:1&lt;/code&gt; and &lt;code&gt;PKG C:2&lt;/code&gt; at the same time in a project running system. &lpar;Just think of past decades. No advanced package managers&rpar;&lt;/p&gt;
&lt;p&gt;Let&#39;s see how you might break the packages and run into conflict situations.&lt;/p&gt;
&lt;h3 id=&quot;heading-chain-of-conflicts&quot;&gt;Chain of Conflicts&lt;/h3&gt;
&lt;p&gt;We learned about dependencies and how our dependencies might get chained together. So, let&#39;s see a simple conflict that might happen in any project.&lt;/p&gt;
&lt;p&gt;We have our &lt;code&gt;App&lt;/code&gt; already designed on the left hand side. Our application depends on &lt;code&gt;PKG A:1&lt;/code&gt; and &lt;code&gt;PKG B:1&lt;/code&gt; and both of those requirements are depending on &lt;code&gt;PKG C:1&lt;/code&gt; so far.&lt;/p&gt;
&lt;p&gt;&lt;img src=&quot;https://cdn.hashnode.com/res/hashnode/image/upload/v1653570625836/vLqVEy33E.png&quot; alt=&quot;Artboard 1@4x.png&quot; class=&quot;image--center mx-auto&quot; /&gt;&lt;/p&gt;
&lt;p&gt;Everything sounds cool and clean. After a few weeks, &lt;code&gt;PKG A:1&lt;/code&gt; maintainers find a horrific security bug in their package and after a few days, they release &lt;code&gt;PKG A:2&lt;/code&gt; with a higher security layer and they fix the issues.&lt;/p&gt;
&lt;p&gt;Since we care about the security of our project, we decide to upgrade our &lt;code&gt;PKG A:1&lt;/code&gt; to &lt;code&gt;PKG A:2&lt;/code&gt; for fewer possible security threats and that&#39;s what happens!!&lt;/p&gt;
&lt;p&gt;&lt;img src=&quot;https://cdn.hashnode.com/res/hashnode/image/upload/v1653570532093/NnNYG9Rpt.png&quot; alt=&quot;Artboard 1@4x.png&quot; class=&quot;image--center mx-auto&quot; /&gt;&lt;/p&gt;
&lt;p&gt;As we described earlier, we can&#39;t keep two different versions of the same package in a running system. Once we prepare the &lt;code&gt;PKG A:2&lt;/code&gt;, we see that the new &lt;code&gt;PKG A:2&lt;/code&gt; now depends on &lt;code&gt;PKG C:2&lt;/code&gt; which was &lt;code&gt;PKG C:1&lt;/code&gt; in the previous version of &lt;code&gt;PKG A&lt;/code&gt;. Since our &lt;code&gt;PKG B:1&lt;/code&gt; still depends on &lt;code&gt;PKG C:1&lt;/code&gt;, how can we prepare both &lt;code&gt;PKG A:2&lt;/code&gt; and &lt;code&gt;PKG B:1&lt;/code&gt; at the same time?!&lt;/p&gt;
&lt;p&gt;Well, that&#39;s a simple versioning conflict. Today, package managers have their own algorithms for facing such a situation. In an upgrade situation, before they touch anything, they read from the databases and check for any possible conflict in the system. They draw the graphs, analyze the packages, and check the routes, and their last step will be upgrading/downgrading/installation or even uninstallation processes. That&#39;s a good convention but how this conflict can be solved?&lt;/p&gt;
&lt;p&gt;As a maintainer, we can wait for a new release from &lt;code&gt;PKG C&lt;/code&gt; which would probably support both &lt;code&gt;PKG B:1&lt;/code&gt; and &lt;code&gt;PKG A:2&lt;/code&gt;. Like we have to keep those threats till the new release comes out from the &lt;code&gt;PKG C&lt;/code&gt; maintainers or even we can touch nothing and keep those threats on the hush!&lt;/p&gt;
&lt;p&gt;&lt;img src=&quot;https://cdn.hashnode.com/res/hashnode/image/upload/v1653570773139/nTfRNj8he.png&quot; alt=&quot;Artboard 1@4x.png&quot; class=&quot;image--center mx-auto&quot; /&gt;&lt;/p&gt;
&lt;p&gt;Also, there might be a new release as &lt;code&gt;PKG C:1.0.1&lt;/code&gt; which is actually a minor change for supporting both packages. It actually backs to the maintainers&#39; choice.&lt;/p&gt;
&lt;h3 id=&quot;heading-circular-dependency&quot;&gt;Circular Dependency&lt;/h3&gt;
&lt;p&gt;There is another situation where our dependencies depend on each other. In the following situation, the package &lt;code&gt;PKG Q:3&lt;/code&gt; only works if &lt;code&gt;PKG Z:5&lt;/code&gt; works as well and vice versa. On the other hand, we have the package &lt;code&gt;PKG F:1&lt;/code&gt; which depends on &lt;code&gt;PKG S:4&lt;/code&gt;, and the package &lt;code&gt;PKG S:4&lt;/code&gt; can&#39;t work without &lt;code&gt;PKG F:1&lt;/code&gt;.&lt;/p&gt;
&lt;p&gt;&lt;img src=&quot;https://cdn.hashnode.com/res/hashnode/image/upload/v1653576441730/f2r7v_gZo.png&quot; alt=&quot;Artboard 1@4x.png&quot; class=&quot;image--center mx-auto&quot; /&gt;&lt;/p&gt;
&lt;p&gt;In this situation, we have a circular dependency on each package. If one breaks, the other one won&#39;t work anymore.&lt;/p&gt;
&lt;p&gt;Now, let&#39;s describe the solutions and best practices to keep the hell&#39;s door closed.&lt;/p&gt;
&lt;h3 id=&quot;heading-package-managers-microservices-andamp-project-level-tests-solutions&quot;&gt;Package Managers, Microservices &amp;amp; Project-level Tests Solutions&lt;/h3&gt;
&lt;p&gt;In the monolithic infrastructures, there is way more possibility of having conflicts since we are serving the whole service from the same running system and scope. In the microservice structures, we have our services separated from each other so then we don&#39;t care about each service&#39;s dependencies since they are responsible for their own requirements. In this structure, debugging the issues would be way easier because we are talking about a smaller scope and service. That&#39;s actually another meaning of having isolated services. They have their developers, resources, tests, package managers, and so on.&lt;/p&gt;
&lt;p&gt;Thinking of package managers. They are smart tools for managing the dependencies and they have advanced implementations to avoid any conflict on our machines.&lt;/p&gt;
&lt;p&gt;Even nowadays, you can find some package managers still can&#39;t actually solve the conflict issues among the packages and their dependencies. In most cases, they suggest you the reinstallation process which is truly painful.&lt;/p&gt;
&lt;p&gt;You might have been working with multiple package managers such as &lt;a target=&quot;_blank&quot; href=&quot;https://wiki.archlinux.org/title/pacman&quot;&gt;Pacman&lt;/a&gt;, &lt;a target=&quot;_blank&quot; href=&quot;https://ubuntu.com/server/docs/package-management&quot;&gt;APT&lt;/a&gt;, &lt;a target=&quot;_blank&quot; href=&quot;https://www.redhat.com/sysadmin/how-manage-packages&quot;&gt;YUM&lt;/a&gt;, or other ones. You can read about their history to find how they&#39;ve been solving the different issues on the different machines. Choosing the right package managers &lpar;officially announced ones&rpar; would be the key to the dependency paradise!&lt;/p&gt;
&lt;p&gt;Last but not least, a great solution to your dependency issues is writing tests for your projects. When your project has its own tests, it&#39;s actually testable in the different environments and situations. You can easily test your project with the different versions of packages and dependencies. Most testing tools will also notify you the news about the deprecation, substitutions, and things that might affect some of your project&#39;s features after the upgrade process.&lt;/p&gt;
&lt;h3 id=&quot;heading-conclusion&quot;&gt;Conclusion&lt;/h3&gt;
&lt;p&gt;In this article, we described a simple situation where a tiny bit of dependency conflict might happen in the system. Then we moved to the conventions and solutions. Nowadays, with the rise of the powerful package management tools, we may never feel those conflicts anymore.&lt;/p&gt;
<!-- BLOGPOSTS:END -->

Check out [__imsadra.me__](https://imsadra.me) for more posts and blogs.

</samp>

#### :call_me_hand: Contact Me
<samp>
  
[__Twitter__](https://twitter.com/lnxpylnxpy) | [__Email__](mailto:lnxpylnxpy@gmail.com) | [__Weblog__](https://imsadra.me) | [__LinkedIn__](https://www.linkedin.com/in/ali-reza-yahyapour-18b896164/)
  
</samp>
