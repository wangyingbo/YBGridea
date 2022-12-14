---
title: 'How Do I Declare A Block in Objective-C?'
date: 2022-07-06 17:39:12
tags: []
published: true
hideInList: false
feature: 
isTop: false
---


<!DOCTYPE html>
<html>

<head>
<meta http-equiv="Content-Type" content="text/html; charset=utf-8">

  <title>How Do I Declare A Block in Objective-C?</title>
  <style>body {
      background-color: #002b36;
      color: #839496;
      font-family: Lucida Grande, sans-serif;
      font-size: 20px;
      padding: 40px;
      padding-bottom: 0;
    }

    strong {
      color: #268bd2;
    }

    h1 {
      font-size: 40px;
      margin-bottom: 1.5em;
      text-align: center;
    }

    h2 {
      font-weight: normal;
    }

    .return {
      color: #2aa198;
    }

    .name {
      color: #BC8800;
    }

    .parameter-types, .parameters {
      color: #7C9F00;
    }
    
    .nullability {
      color: #EC407A;
    }

    .disclaimer {
      line-height: 2em;
    }

    code {
      display: block;
      font-family: Monaco, Menlo, monospace;
      font-size: 20px;
      margin-bottom: 3em;
      margin-left: 40px;
      margin-top: 1.5em;
    }

    footer {
      font-size: 12px;
      margin-top: 200px;
      opacity: 0.4;
      text-align: right;
    }

    a {
      color: #0088D9;
      text-decoration: none;
    }

  </style>

  <style media="print">body {
      background-color: #FFFFFF;
      font-size: 16px;
      padding: 20px;
    }

    h1 {
      font-size: 28px;
      margin-bottom: 1em;
    }

    code {
      font-size: 16px;
      margin-bottom: 2em;
      margin-left: 20px;
    }

    footer {
      font-size: 10px;
      margin-top: 40px;
    }
  </style>

  <link rel="apple-touch-icon" sizes="57x57" href="apple-touch-icon-57x57.png">
  <link rel="apple-touch-icon" sizes="114x114" href="apple-touch-icon-114x114.png">
  <link rel="apple-touch-icon" sizes="72x72" href="apple-touch-icon-72x72.png">
  <link rel="apple-touch-icon" sizes="144x144" href="apple-touch-icon-144x144.png">
  <link rel="apple-touch-icon" sizes="60x60" href="apple-touch-icon-60x60.png">
  <link rel="apple-touch-icon" sizes="120x120" href="apple-touch-icon-120x120.png">
  <link rel="apple-touch-icon" sizes="76x76" href="apple-touch-icon-76x76.png">
  <link rel="apple-touch-icon" sizes="152x152" href="apple-touch-icon-152x152.png">
  <link rel="icon" type="image/png" href="favicon-196x196.png" sizes="196x196">
  <link rel="icon" type="image/png" href="favicon-160x160.png" sizes="160x160">
  <link rel="icon" type="image/png" href="favicon-96x96.png" sizes="96x96">
  <link rel="icon" type="image/png" href="favicon-16x16.png" sizes="16x16">
  <link rel="icon" type="image/png" href="favicon-32x32.png" sizes="32x32">

  <link rel="mask-icon" href="pinned-tab.svg" color="#002b36">

</head>

<body>
  <h1>How Do I Declare A Block in Objective-C?</h1>

  <div>
    <h2>As a <strong>local variable</strong>:</h2>
    <code>
      <span class="return">returnType</span> (^<span class="name">blockName</span>)(<span class="parameter-types">parameterTypes</span>) = ^<span class="return">returnType</span>(<span class="parameters">parameters</span>) {...};
    </code>
  </div>

  <div>
    <h2>As a <strong>property</strong>:</h2>
    <code>
      @property (nonatomic, copy, <span class="nullability">nullability</span>) <span class="return">returnType</span> (^<span class="name">blockName</span>)(<span class="parameter-types">parameterTypes</span>);
    </code>
  </div>

  <div>
    <h2>As a <strong>method parameter</strong>:</h2>
    <code>
      - (void)someMethodThatTakesABlock:(<span class="return">returnType</span> (^<span class="nullability">nullability</span>)(<span class="parameter-types">parameterTypes</span>))<span class="name">blockName</span>;
    </code>
  </div>

  <div>
    <h2>As an <strong>argument to a method call</strong>:</h2>
    <code>
      [someObject someMethodThatTakesABlock:^<span class="return">returnType</span> (<span class="parameters">parameters</span>) {...}];
    </code>
  </div>
  
  <div>
    <h2>As a <strong>parameter to a C function</strong>:</h2>
    <code>
      void SomeFunctionThatTakesABlock(<span class="return">returnType </span>(^<span class="name">blockName</span>)(<span class="parameter-types">parameterTypes</span>));<br/>
    </code>
  </div>

  <div>
    <h2>As a <strong>typedef</strong>:</h2>
    <code>
      typedef <span class="return">returnType</span> (^<span class="name">TypeName</span>)(<span class="parameter-types">parameterTypes</span>);<br/>
      <span class="name">TypeName</span> blockName = ^<span class="return">returnType</span>(<span class="parameters">parameters</span>) {...};
    </code>
  </div>

  <div class="disclaimer">
    This site is not intended to be an exhaustive list of all possible uses of blocks.<br>
    If you find yourself needing syntax not listed here, it is likely that a <strong>typedef</strong> would make your
    code more readable.<br>
    <br>
    Unable to access this site due to the profanity in the URL? <strong><a href="http://goshdarnblocksyntax.com">http://goshdarnblocksyntax.com</a></strong>
    is a more work-friendly mirror.
  </div>

  <footer>By <a href="http://lazerwalker.com">Em Lazer-Walker</a>, who has a very bad memory for this sort of thing.<br />
    Like this site? Consider throwing me a few bucks via <a href='https://ko-fi.com/A2223KQN'>Ko-fi</a>.</footer>

  <script>
    (function (i, s, o, g, r, a, m) {
      i['GoogleAnalyticsObject'] = r; i[r] = i[r] || function () {
        (i[r].q = i[r].q || []).push(arguments)
      }, i[r].l = 1 * new Date(); a = s.createElement(o),
        m = s.getElementsByTagName(o)[0]; a.async = 1; a.src = g; m.parentNode.insertBefore(a, m)
    })(window, document, 'script', '//www.google-analytics.com/analytics.js', 'ga');

    ga('create', 'UA-43658906-1', 'fuckingblocksyntax.com');
    ga('send', 'pageview');
  </script>

</body>

</html>
