# Pyscript-Playground
Just a little playground to explore PyScript

## (A) well.html
<b>A test to see if I could get Welly or Lasio to run via Pyscript</b>
Live at: https://justingosses.github.io/pyscript-playground/well.html use console to see print statements

#### Current Bug
Initial test didn't work, but think I know why. Welly uses Lasio to load LAS files. LASIO uses urllib/requests.py to load files.

Apparently the way urllib makes requests doesn't work well with WASM. 

The details are fuzzy but other people have hit same problem as shown here: https://community.anaconda.cloud/t/the-requests-module/20494 and here: https://community.anaconda.cloud/t/patching-a-pure-python-package-that-uses-requests/20427

It seems this issue is being worked from last comment but unclear if there's a path forward generally. 

#### (B) Alternative Methods of Loading Well Files?
An alternative for well files might be to (1) leverage wellio.js to load the file as either a string or JSON and then (2) pass that to Wellio or LASIO?

This "should" work, but I currently don't understand and/or remember much about conversion between the different JSON types (wellio vs. LASIO) as well as Welly's ability to to load LAS files via JSON instead of LAS files???? Relevant links are <a href="https://github.com/agilescientific/welly/issues/79">this issue on Welly about JSON conversion</a> and <a href="https://justingosses.github.io/wellio.js/docs/#wellio-style-json-vs-others">this part of Wellio.js's docs that covers conversion between Wellio and LASIO JSON formats.</a>

Also, there' PyFetch, which seems to be what some people are recommending be used instead of requests and URLLIB2. An small example is here: https://github.com/pyscript/pyscript/pull/151/files

#### (C) well_from_scratch.html
In this one, which is live at https://justingosses.github.io/pyscript-playground/well_from_scratch.html , a LAS file is created from scratch using lasio.
This avoids the problem of loading files and as  a result we can see both LASIO and WELLY work!. 

All I do is print some text from the LAS, but it works.

#### (D) Welly and Lasio working with hardcoded string of a LAS well file: WORKS!
https://justingosses.github.io/pyscript-playground/welly_hardCodedLasString_works.html

This page shows a demo of Welly working successfully with a hard coded string version of a LAS file. 

It even prints a figure, leveraging matplotlib, to the HTML page. 

Next step will be to use Wellio.js and some JavaScript to build a user interface that lets users load LAS well files from arbitrary locations.

#### (E) welly_LASfile_notWorking.html - Attempt at Running Wellio.js and Pyscript in Same Page
This was an attempt at Running Wellio.js and Pyscript in Same Page.

It didn't work because I wanted to call require.js to call wellio.js and doing so breaks PySCript. 

I suspect because PyScript JS also calls require.js? More explained in the HTML of welly_LASfile_notWorking.html

For comparison, the HTML file welly_hardCodedLasString_works.html is nearly identical to this one but doesn't load require.js. 
In fact, if you do nothing more to welly_hardCodedLasString_works.html except add  <script src="https://cdnjs.cloudflare.com/ajax/libs/require.js/2.3.6/require.min.js"></script>, it breaks and the error in the console is: `Uncaught (in promise) ReferenceError: loadPyodide is not defined
    at loadInterpreter (interpreter.ts:418:5)
    at HTMLScriptElement.initializePyodide (App.svelte:16:31)`.

#### (F) THIS ONE WORKS: welly_LASfile_wAjax.html

Uses Ajax from jquery to do the loading from the LAS file here and it works fine.

## Status of This Work

This is getting into the rats nest phase. No offense to rats. Might come back to it and maybe not.