
fs = require 'fs'
path = require 'path'
glob = require 'glob'

print = console.log
after = (ms, fn)-> setTimeout(fn, ms)
every = (ms, fn)-> setInterval(fn, ms)

tab = (str)->
	# Indent the output. Because I care.
	str.replace(/\n/g, '\n\t')

boil = ({title, head, body})->
	# Boilerplate and stuff.
	# A Template, really. But I like 'boiling', like I'm cooking webpages.
	# ...before serving them... yes...
	# I don't use any of that nasty phpreprocessed stuff.
	"""
		<!doctype html>
		<html lang="en-US">
			<head>
				<meta charset="utf-8">
				<meta name="author" content="Isaiah Odhner">
				<meta name="description" content="Isaiah Odhner's portfolio website">
				<meta name="keywords" content="Isaiah Odhner, 1j0, 1j01">
				<meta name="viewport" content="width=device-width, initial-scale=1">
				<title>#{if title then "#{title} — " else ""}Isaiah Odhner</title>
				<link rel="stylesheet" type="text/css" href="portfolio.css">
				<link rel="stylesheet" type="text/css" href="https://cdnjs.cloudflare.com/ajax/libs/octicons/2.1.2/octicons.css">
				<script src="global.coffee" type="text/coffeescript"></script>
				#{tab tab (head ? "")}
			</head>
			<body>
				<header>
					<h1>Isaiah Odhner</h1>
					<nav>
						<a href="/">Projects</a>
						<a href="mailto:isaiahodhner@gmail.com">Contact</a>
					</nav>
				</header>
				#{tab tab body}
				<footer></footer>
				<script src="lib/coffee-script.js"></script>
			</body>
		</html>
	"""

Array::conjunct = (conjunction)->
	if @length > 0
		[most..., last] = @
		"#{most.join(", ")} #{conjunction} #{last}"
	else
		@[0]

log_divisibles = (n, unit, more_info...)->
	nondivisibles = []
	divisibles = []
	(if n / i is n // i then divisibles else nondivisibles).push i for i in [1..10]
	console.log "
		#{n} #{unit},
		divisible by #{divisibles.conjunct "and"},
		but not by #{nondivisibles.conjunct "or"}
	", more_info...

task 'boil', 'Build the website, boiling the pages.', ->
	
	pattern_fnames = glob.sync 'images/patterns/*.png'
	
	log_divisibles pattern_fnames.length, "pattern tiles"
	
	pattern_images = (
		for fname in pattern_fnames
			"""
				<article itemscope itemtype="http://schema.org/ImageObject">
					<img src="#{fname}" itemprop="contentURL">
				</article>
			"""
	).join ''
	
	fs.writeFileSync 'patterns.html', boil
		title: 'Patterns'
		head: '<script src="patterns.coffee" type="text/coffeescript"></script>'
		body: """
			<p>
				These are some patterns I made with code and a tool that made with code.
			</p>
			<div id="patterns">
				#{tab pattern_images}
			</div>
		"""
	
	projects =
		'audio-editor':
			name: 'Audio Editor'
			description: 'An online digital audio worksation'
			url: 'https://audioeditor.ml'
		'tri-chromatic-keyboard':
			name: 'Tri-Chromatic Keyboard'
			description: 'Better than a regular keyboard'
		'guitar':
			name: 'Guitar'
			description: 'Easily play and record tabs'
			bg: "light"
		'choon.js':
			name: 'Choon.js'
			description: 'Choon language interpreter built with the Web Audio API'
		'rtttl.js':
			name: 'RTTTL.js'
			description: 'Play a bunch of ringtones'
		'jspaint':
			name: 'JS Paint'
			description: 'Classic MS Paint, revived +Transparency +Unlimited Undos'
		'project-nexus':
			name: 'Project Nexus'
			description: 'A hub for all your coding projects'
			url: 'repo'
		'multifiddle':
			name: 'MultiFiddle'
			description: 'Minimalistic multiplayer live code fiddling environment'
		'mind-map':
			name: 'MindMap'
			description: 'Map your mind without ugly boxes'
			bg: "light"
		'transpairency':
			name: 'Trans<em>pair</em>ency'
			description: 'B&W to transparent'
			bg: "light"
		'tiamblia':
			name: 'Tiamblia'
			description: 'A notagame'
		'slugg':
			name: 'SLUGG'
			description: 'A simple little up-going game'
		'mos':
			name: 'MOS'
			description: 'Monochrome Operating System'
		'1bpp':
			name: 'One Bit Per Pixel'
			description: 'A notagame in pure B&W'
		'board-game':
			name: 'Chance'
			description: 'A board game?'
		'une':
			name: 'UNE: The Complete Multitool'
			description: 'An incomplete unitool for a game called 5UNE17A'
		'stick-mangler':
			name: 'Stick Mangler'
			description: 'Not Stick Ranger'
		'pool':
			name: 'Jussom Billiards'
			description: 'Just playing around with physics'
		'pipes':
			name: 'Pipes'
			description: '3d pipes screensaver remake'
		'boxart':
			name: 'BoxArt'
			description: '3d drag & drop box art generator'
		'babble':
			name: 'Babble'
			description: 'Sentence generator and more'
			bg: "light"
		'patterns':
			name: 'Patterns'
			description: 'Procedurally generated patterns'
			url: 'patterns'
			repo_url: 'https://github.com/1j01/1j01.github.io'
		'gif-maker':
			name: 'GIF Maker'
			description: 'Make animated GIF images'
		'countdown.ml':
			name: 'Countdown.ml'
			description: 'What does it look like?'
			bg: "light"
		'font-detective':
			name: 'Font Detective'
			description: 'Detects fonts in browser'
			bg: "light"
		'>> 98': # really this whole data structure should be an array; this is a hack to place this item
			name: '98'
			description: 'Windows 98 desktop remake'
		'pesterchum':
			name: 'PesterChum'
			description: 'MS Paint Adventures chat client'
			url: 'repo'
		'sbahjifier':
			name: 'SBAHJifier'
			description: 'Make any page look like SWEET BRO AND HELLA JEFF'
			url: 'https://chrome.google.com/webstore/detail/sbahjifier/gejobhmmpioknjihlhemplpfchbnbpin'
	
	log_divisibles Object.keys(projects).length, "project tiles", "(before tiles are spanned)"
	
	fs.writeFileSync 'index.html', boil
		head: '<script src="project-tiles.coffee" type="text/coffeescript"></script>'
		body: (
			
			for key, project of projects
				key = key.replace ">> ", ""
				
				repo_url = project.repo_url ? "https://github.com/1j01/#{key}"
				gh_pages_url = "http://1j01.github.io/#{key}/"
				url =
					if project.url is 'repo'
						repo_url
					else
						project.url ? gh_pages_url
				
				bg = project.bg ? "normal"
				sizes = ["1x1"] if fs.existsSync "images/projects/#{key}.png"
				for img_path in glob.sync "images/projects/#{key}-*.png"
					m = img_path.match /-(\d+x\d+)\./
					sizes.push m[1] if m
				
				"""
					<article itemscope itemtype="http://schema.org/WebPage" data-bg="#{bg}" data-sizes="#{sizes}">
						<a href="#{url}" itemprop="url">
							<img itemprop="image" width=256 height=256 src="images/projects/#{key}.png">
						</a>
						<header itemprop="name">
							<a href="#{repo_url}" class="repo" title="View repository on Github"><span class="octicon octicon-repo"></span></a>
							<span>#{project.name}</span>
						</header>
						<footer itemprop="description">#{project.description}</footer>
					</article>
				"""
				
		).join ''


task 'optimages', 'Optimize all the images.', ->
	
	optimage = require 'optimage'
	
	glob '**/*.png', (err, files)->
		if err
			print err
		else
			do fn = (i = 0)->
				next = ->
					if i + 1 < files.length
						fn i + 1
				
				f = files[i]
				
				if f.match /node_modules/
					do next
				else
					optimage {
						inputFile: f
						outputFile: f
					}, (err, res)->
						
						if err
							print "#{f} ::: ERROR"
							print err
							print "\n"
						else
							if (res.stderr.indexOf 'already optimized') isnt -1 or res.saved < 10
								print "#{f} ::: already optimized"
							else
								print "#{f} ::: saved #{res.saved} bytes"
						
						do next

task 'e', 'Edit a tiled version of a pattern in photoshop.', (options)->
	# haha this whole thing is so overkill
	
	cd = fs.realpathSync "."
	temp = "#{cd}/temp"
	try fs.mkdirSync temp
	
	gm = require 'gm'
	cp = require 'child_process'
	readline = require 'readline'
	optimage = require 'optimage'
	
	rl = readline.createInterface
		input: process.stdin
		output: process.stdout
	
	rl.setPrompt "> "
	rl.question "Please enter the filename (extension optional) of an image in 1j01.github.io/images/patterns/", (f)->
		f = f.replace ".png", ""
		rl.close()
		
		PsDir = "C:/Program Files (x86)/Adobe/Adobe Photoshop CS2"
		Photoshop = "#{PsDir}/Photoshop.exe"
		ImageReady = "#{PsDir}/ImageReady.exe"
		
		originalFilePath = path.normalize "#{cd}/images/patterns/#{f}.png"
		tiledFilePath = path.normalize "#{temp}/#{f}-tiled.png"
		newFilePath = path.normalize "#{cd}/images/patterns/#{f}-psedit.png"
		
		print "Editing a tiled version of #{originalFilePath}"
		
		fs.exists originalFilePath, (exists)->
			if not exists
				print "ERROR: #{originalFilePath} does not exist."
			else
				
				img = gm()
				
				# Tile the pattern (there might be an option (-tile) for this, but whatever: the documentation is terrible and this works)
				w = h = 512
				for x in [0...3]
					for y in [0...3]
						img.in '-page', "+#{x*w}+#{y*h}"
						img.in originalFilePath
				
				# Merge the images as a matrix
				img.mosaic()
				
				# Write the file
				img.write tiledFilePath, (err)->
					if err
						print """
						
						
						Is GraphicsMagic installed and in the path and computer restarted and stuff?
						You need the Q8 version btw.
						DSWYFT
						
						
						"""
						# Why do I have such detailed error handling in my portfolio website's Cakefile? idk
						# I don't remember what DSWYFT stands for. It's a TANSA. (a Thoughtless And Non-Standard Accronym)
						return console.error err
					
					# Sometimes gm calls back without having written a file, maybe this helps. Probably not.
					after 50, ->
						
						fs.chmod tiledFilePath, 0o777, (err)->
							if err
								print "chmod 777 ::: ERROR"
								return console.error err
							
							cp.spawn Photoshop, [tiledFilePath], cwd: (require 'path').dirname(tiledFilePath)
							
							fs.watch tiledFilePath, ->
								gm()
								.in(tiledFilePath)
								.crop(w, h, w, h) # (width, height, x, y)!? :(
								.write newFilePath, (err)->
									if err
										print "gm.write() error"
										return console.error err
									else
										# regenerate patterns.html in case there's a new pattern
										invoke 'boil'
										# optimize the new image
										optimage {
											inputFile: newFilePath
											outputFile: newFilePath
										}, (err, res)->
											
											if err
												print "Optimizing #{newFilePath} ::: ERROR"
												print err
												print "\n"
											else
												if (res.stderr.indexOf 'already optimized') isnt -1 # or res.saved < 10
													print "Optimizing #{newFilePath} ::: already optimized??"
												else
													print "Optimizing #{newFilePath} ::: saved #{res.saved} bytes"


task 'sbuild', '(invokes boil) invoked by Ctrl+B in Sublime Text', -> invoke 'boil'
task 'build', '(invokes boil)', -> invoke 'boil'

