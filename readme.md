## Electron

```
PM> Install-Package ElectronNET.API

<h2><a id="user-content-programcs" class="anchor" aria-hidden="true" href="#programcs"><svg class="octicon octicon-link" viewBox="0 0 16 16" version="1.1" width="16" height="16" aria-hidden="true"><path fill-rule="evenodd" d="M4 9h1v1H4c-1.5 0-3-1.69-3-3.5S2.55 3 4 3h4c1.45 0 3 1.69 3 3.5 0 1.41-.91 2.72-2 3.25V8.59c.58-.45 1-1.27 1-2.09C10 5.22 8.98 4 8 4H4c-.98 0-2 1.22-2 2.5S3 9 4 9zm9-3h-1v1h1c1 0 2 1.22 2 2.5S13.98 12 13 12H9c-.98 0-2-1.22-2-2.5 0-.83.42-1.64 1-2.09V6.25c-1.09.53-2 1.84-2 3.25C6 11.31 7.55 13 9 13h4c1.45 0 3-1.69 3-3.5S14.5 6 13 6z"></path></svg></a>Program.cs</h2>
<p>You start Electron.NET up with an <code>UseElectron</code> WebHostBuilder-Extension.</p>
<div class="highlight highlight-source-cs"><pre><span class="pl-k">public</span> <span class="pl-k">static</span> <span class="pl-en">IWebHost</span> <span class="pl-en">BuildWebHost</span>(<span class="pl-k">string</span>[] <span class="pl-smi">args</span>)
{
    <span class="pl-k">return</span> <span class="pl-smi">WebHost</span>.<span class="pl-en">CreateDefaultBuilder</span>(<span class="pl-smi">args</span>)
        .<span class="pl-en">UseStartup</span>&lt;<span class="pl-en">Startup</span>&gt;()
        .<span class="pl-en">UseElectron</span>(<span class="pl-smi">args</span>)
        .<span class="pl-en">Build</span>();
}</pre></div>
<h2><a id="user-content-startupcs" class="anchor" aria-hidden="true" href="#startupcs"><svg class="octicon octicon-link" viewBox="0 0 16 16" version="1.1" width="16" height="16" aria-hidden="true"><path fill-rule="evenodd" d="M4 9h1v1H4c-1.5 0-3-1.69-3-3.5S2.55 3 4 3h4c1.45 0 3 1.69 3 3.5 0 1.41-.91 2.72-2 3.25V8.59c.58-.45 1-1.27 1-2.09C10 5.22 8.98 4 8 4H4c-.98 0-2 1.22-2 2.5S3 9 4 9zm9-3h-1v1h1c1 0 2 1.22 2 2.5S13.98 12 13 12H9c-.98 0-2-1.22-2-2.5 0-.83.42-1.64 1-2.09V6.25c-1.09.53-2 1.84-2 3.25C6 11.31 7.55 13 9 13h4c1.45 0 3-1.69 3-3.5S14.5 6 13 6z"></path></svg></a>Startup.cs</h2>
<p>Open the Electron Window in the Startup.cs file:</p>
<div class="highlight highlight-source-cs"><pre><span class="pl-k">public</span> <span class="pl-k">void</span> <span class="pl-en">ConfigureServices</span>(<span class="pl-en">IServiceCollection</span> <span class="pl-smi">services</span>)
{            
    <span class="pl-smi">services</span>.<span class="pl-en">AddMvc</span>(<span class="pl-smi">option</span> <span class="pl-k">=&gt;</span> <span class="pl-smi">option</span>.<span class="pl-smi">EnableEndpointRouting</span> <span class="pl-k">=</span> <span class="pl-c1">false</span>);
}

<span class="pl-k">public</span> <span class="pl-k">void</span> <span class="pl-en">Configure</span>(<span class="pl-en">IApplicationBuilder</span> <span class="pl-smi">app</span>, <span class="pl-en">IHostingEnvironment</span> <span class="pl-smi">env</span>)
{
    <span class="pl-k">if</span> (<span class="pl-smi">env</span>.<span class="pl-en">IsDevelopment</span>())
    {
        <span class="pl-smi">app</span>.<span class="pl-en">UseDeveloperExceptionPage</span>();
        <span class="pl-smi">app</span>.<span class="pl-en">UseBrowserLink</span>();
    }
    <span class="pl-k">else</span>
    {
        <span class="pl-smi">app</span>.<span class="pl-en">UseExceptionHandler</span>(<span class="pl-s"><span class="pl-pds">"</span>/Home/Error<span class="pl-pds">"</span></span>);
    }

    <span class="pl-smi">app</span>.<span class="pl-en">UseStaticFiles</span>();

    <span class="pl-smi">app</span>.<span class="pl-en">UseMvc</span>(<span class="pl-smi">routes</span> <span class="pl-k">=&gt;</span>
    {
        <span class="pl-smi">routes</span>.<span class="pl-en">MapRoute</span>(
            <span class="pl-smi">name</span>: <span class="pl-s"><span class="pl-pds">"</span>default<span class="pl-pds">"</span></span>,
            <span class="pl-smi">template</span>: <span class="pl-s"><span class="pl-pds">"</span>{controller=Home}/{action=Index}/{id?}<span class="pl-pds">"</span></span>);
    });

    <span class="pl-c"><span class="pl-c">//</span> Open the Electron-Window here</span>
    <span class="pl-smi">Task</span>.<span class="pl-en">Run</span>(<span class="pl-k">async</span> () <span class="pl-k">=&gt;</span> <span class="pl-k">await</span> <span class="pl-smi">Electron</span>.<span class="pl-smi">WindowManager</span>.<span class="pl-en">CreateWindowAsync</span>());
}</pre></div>
<p><strong>Please note:</strong> Currently it is important to use ASP.NET Core with MVC. If you are working with the dotnet CLI, use</p>
<pre><code>dotnet new mvc
</code></pre>
<h2><a id="user-content-start-the-application" class="anchor" aria-hidden="true" href="#start-the-application"><svg class="octicon octicon-link" viewBox="0 0 16 16" version="1.1" width="16" height="16" aria-hidden="true"><path fill-rule="evenodd" d="M4 9h1v1H4c-1.5 0-3-1.69-3-3.5S2.55 3 4 3h4c1.45 0 3 1.69 3 3.5 0 1.41-.91 2.72-2 3.25V8.59c.58-.45 1-1.27 1-2.09C10 5.22 8.98 4 8 4H4c-.98 0-2 1.22-2 2.5S3 9 4 9zm9-3h-1v1h1c1 0 2 1.22 2 2.5S13.98 12 13 12H9c-.98 0-2-1.22-2-2.5 0-.83.42-1.64 1-2.09V6.25c-1.09.53-2 1.84-2 3.25C6 11.31 7.55 13 9 13h4c1.45 0 3-1.69 3-3.5S14.5 6 13 6z"></path></svg></a>Start the Application</h2>
<p>To start the application make sure you have installed the "<a href="https://www.nuget.org/packages/ElectronNET.CLI/" rel="nofollow">ElectronNET.CLI</a>" packages as global tool:</p>
<pre><code>dotnet tool install ElectronNET.CLI -g
</code></pre>
<p>At the first time, you need an Electron.NET project initialization. Type the following command in your ASP.NET Core folder:</p>
<pre><code>electronize init
</code></pre>
<ul>
<li>Now a electronnet.manifest.json should appear in your ASP.NET Core project</li>
<li>Now run the following:</li>
</ul>
<pre><code>electronize start
</code></pre>

<h3><a id="user-content-note" class="anchor" aria-hidden="true" href="#note"><svg class="octicon octicon-link" viewBox="0 0 16 16" version="1.1" width="16" height="16" aria-hidden="true"><path fill-rule="evenodd" d="M4 9h1v1H4c-1.5 0-3-1.69-3-3.5S2.55 3 4 3h4c1.45 0 3 1.69 3 3.5 0 1.41-.91 2.72-2 3.25V8.59c.58-.45 1-1.27 1-2.09C10 5.22 8.98 4 8 4H4c-.98 0-2 1.22-2 2.5S3 9 4 9zm9-3h-1v1h1c1 0 2 1.22 2 2.5S13.98 12 13 12H9c-.98 0-2-1.22-2-2.5 0-.83.42-1.64 1-2.09V6.25c-1.09.53-2 1.84-2 3.25C6 11.31 7.55 13 9 13h4c1.45 0 3-1.69 3-3.5S14.5 6 13 6z"></path></svg></a>Note</h3>
<blockquote>
<p>Only the first electronize start is slow. The next will go on faster.</p>
</blockquote>
<h2><a id="user-content-debug" class="anchor" aria-hidden="true" href="#debug"><svg class="octicon octicon-link" viewBox="0 0 16 16" version="1.1" width="16" height="16" aria-hidden="true"><path fill-rule="evenodd" d="M4 9h1v1H4c-1.5 0-3-1.69-3-3.5S2.55 3 4 3h4c1.45 0 3 1.69 3 3.5 0 1.41-.91 2.72-2 3.25V8.59c.58-.45 1-1.27 1-2.09C10 5.22 8.98 4 8 4H4c-.98 0-2 1.22-2 2.5S3 9 4 9zm9-3h-1v1h1c1 0 2 1.22 2 2.5S13.98 12 13 12H9c-.98 0-2-1.22-2-2.5 0-.83.42-1.64 1-2.09V6.25c-1.09.53-2 1.84-2 3.25C6 11.31 7.55 13 9 13h4c1.45 0 3-1.69 3-3.5S14.5 6 13 6z"></path></svg></a>Debug</h2>
<p>Start your Electron.NET application with the Electron.NET CLI command. In Visual Studio attach to your running application instance. Go in the <strong>Debug</strong> Menu and click on <strong>Attach to Process...</strong>. Sort by your projectname on the right and select it on the list.</p>
<h2><a id="user-content-usage-of-the-electron-api" class="anchor" aria-hidden="true" href="#usage-of-the-electron-api"><svg class="octicon octicon-link" viewBox="0 0 16 16" version="1.1" width="16" height="16" aria-hidden="true"><path fill-rule="evenodd" d="M4 9h1v1H4c-1.5 0-3-1.69-3-3.5S2.55 3 4 3h4c1.45 0 3 1.69 3 3.5 0 1.41-.91 2.72-2 3.25V8.59c.58-.45 1-1.27 1-2.09C10 5.22 8.98 4 8 4H4c-.98 0-2 1.22-2 2.5S3 9 4 9zm9-3h-1v1h1c1 0 2 1.22 2 2.5S13.98 12 13 12H9c-.98 0-2-1.22-2-2.5 0-.83.42-1.64 1-2.09V6.25c-1.09.53-2 1.84-2 3.25C6 11.31 7.55 13 9 13h4c1.45 0 3-1.69 3-3.5S14.5 6 13 6z"></path></svg></a>Usage of the Electron-API</h2>
<p>A complete documentation will follow. Until then take a look in the source code of the sample application:<br>
<a href="https://github.com/ElectronNET/electron.net-api-demos">Electron.NET API Demos</a></p>
<p>In this YouTube video, we show you how you can create a new project, use the Electron.NET API, debug a application and build an executable desktop app for Windows: <a href="https://www.youtube.com/watch?v=nuM6AojRFHk" rel="nofollow">Electron.NET - Getting Started</a></p>
<h2><a id="user-content-build" class="anchor" aria-hidden="true" href="#build"><svg class="octicon octicon-link" viewBox="0 0 16 16" version="1.1" width="16" height="16" aria-hidden="true"><path fill-rule="evenodd" d="M4 9h1v1H4c-1.5 0-3-1.69-3-3.5S2.55 3 4 3h4c1.45 0 3 1.69 3 3.5 0 1.41-.91 2.72-2 3.25V8.59c.58-.45 1-1.27 1-2.09C10 5.22 8.98 4 8 4H4c-.98 0-2 1.22-2 2.5S3 9 4 9zm9-3h-1v1h1c1 0 2 1.22 2 2.5S13.98 12 13 12H9c-.98 0-2-1.22-2-2.5 0-.83.42-1.64 1-2.09V6.25c-1.09.53-2 1.84-2 3.25C6 11.31 7.55 13 9 13h4c1.45 0 3-1.69 3-3.5S14.5 6 13 6z"></path></svg></a>Build</h2>
<p>Here you need the Electron.NET CLI as well. Type the following command in your ASP.NET Core folder:</p>
<pre><code>electronize build /target win
</code></pre>
<p>There are additional platforms available:</p>
<pre><code>electronize build /target win
electronize build /target osx
electronize build /target linux
</code></pre>
<p>Those three "default" targets will produce x64 packages for those platforms.</p>
<p>For certain NuGet packages or certain scenarios you may want to build a pure x86 application. To support those things you can define the desired <a href="https://docs.microsoft.com/en-us/dotnet/core/rid-catalog" rel="nofollow">.NET Core runtime</a>, the <a href="https://github.com/electron-userland/electron-packager/blob/master/docs/api.md#platform">electron platform</a> and <a href="https://github.com/electron-userland/electron-packager/blob/master/docs/api.md#arch">electron architecture</a> like this:</p>
<pre><code>electronize build /target custom win7-x86;win32 /electron-arch ia32 
</code></pre>
<p>The end result should be an electron app under your <strong>/bin/desktop</strong> folder.</p>
<h3><a id="user-content-note-1" class="anchor" aria-hidden="true" href="#note-1"><svg class="octicon octicon-link" viewBox="0 0 16 16" version="1.1" width="16" height="16" aria-hidden="true"><path fill-rule="evenodd" d="M4 9h1v1H4c-1.5 0-3-1.69-3-3.5S2.55 3 4 3h4c1.45 0 3 1.69 3 3.5 0 1.41-.91 2.72-2 3.25V8.59c.58-.45 1-1.27 1-2.09C10 5.22 8.98 4 8 4H4c-.98 0-2 1.22-2 2.5S3 9 4 9zm9-3h-1v1h1c1 0 2 1.22 2 2.5S13.98 12 13 12H9c-.98 0-2-1.22-2-2.5 0-.83.42-1.64 1-2.09V6.25c-1.09.53-2 1.84-2 3.25C6 11.31 7.55 13 9 13h4c1.45 0 3-1.69 3-3.5S14.5 6 13 6z"></path></svg></a>Note</h3>
<blockquote>
<p>macOS builds can't be created on Windows machines because they require symlinks that aren't supported on Windows (per <a href="https://github.com/electron-userland/electron-packager/issues/71">this Electron issue</a>). macOS builds can be produced on either Linux or macOS machines.</p>
</blockquote>
<h1><a id="user-content-working-with-this-repo" class="anchor" aria-hidden="true" href="#working-with-this-repo"><svg class="octicon octicon-link" viewBox="0 0 16 16" version="1.1" width="16" height="16" aria-hidden="true"><path fill-rule="evenodd" d="M4 9h1v1H4c-1.5 0-3-1.69-3-3.5S2.55 3 4 3h4c1.45 0 3 1.69 3 3.5 0 1.41-.91 2.72-2 3.25V8.59c.58-.45 1-1.27 1-2.09C10 5.22 8.98 4 8 4H4c-.98 0-2 1.22-2 2.5S3 9 4 9zm9-3h-1v1h1c1 0 2 1.22 2 2.5S13.98 12 13 12H9c-.98 0-2-1.22-2-2.5 0-.83.42-1.64 1-2.09V6.25c-1.09.53-2 1.84-2 3.25C6 11.31 7.55 13 9 13h4c1.45 0 3-1.69 3-3.5S14.5 6 13 6z"></path></svg></a>Working with this Repo</h1>