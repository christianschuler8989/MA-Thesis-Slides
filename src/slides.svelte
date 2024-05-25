<script lang="ts">
	import { Presentation, Slide, Media, FitText, Step, Stack, Code, Notes } from '@components'
	import Layout from './layout.svelte'
</script>

<!-- Typical Errors
	
	"Uncaught TypeError: slidesInChapter[0] is undefined" and layout elements missing.
	→ This can happen if a chapter is defined but has no slides.

-->

<Presentation>	
	<script>
		// information about this presentation 
		const author = "Christian Schuler"; 
		const authorshort = "Schuler"; 
		const title = "Neural Machine Translation for Low-Resource Language Variations on Synthetic Data by Incorporating Linguistic Information";
		const subtitle = "Master's Thesis";
		const department = "Department of Informatics"; 
		const university = "University of Hamburg"; 
		var currentChapterName="";
		var currentChapterNumber=0;
		var chapterNames=[];
		var toc = false;  // whether toc is to be generated
		// data structure: [chapter number, chapter name, slideID]
		var presentationData = []; 
		function newChapter(chapterName){
			currentChapterName=chapterName; 
			currentChapterNumber++;
			chapterNames.push(chapterName);
		}
		// called when new slide is created
		var page=0; 
		function newPage(){
			page++; //note that page n has index n-1
			presentationData.push({chapternr: currentChapterNumber, chapter:currentChapterName,pagenr:page});
		}
	</script>

	<!-- title page -->
	<Slide><Layout>
		<div class="m-16 flex h-[30vh] w-[95vw] bg-[var(--themecolor)] text-white items-center justify-center gap-[100px]">
			<div>
				<div class="text-[6vh]">
					<span id="mytitle"> </span>
				</div>
				<br>
				<div class="text-[4vh]">
					<span id="mysubtitle"> </span>
				</div>
			</div>
		</div>
		<br>
		<div> 
			<span id="myname"></span>
		</div>
		<br>
		<div class="text-[3vh]"> 
			<span id="myuni"></span>
		</div>
		<div class="flex items-center justify-center">
			<img class="h-[18vh] align-middle" src="up-uhh-logo-u-2010-u-png.png" alt="uhh logo">
		</div>
		<div class="text-[2.5vh]"> 
			<br>
			<span id="mydate"></span>
		</div>
		
		
		<!-- fill in the data for this presentation  -->
		<script> 
			document.getElementById("mytitle").innerHTML=title;
			document.getElementById("mysubtitle").innerHTML=subtitle;
			document.getElementById("myname").innerHTML=author;
			document.getElementById("myuni").innerHTML=department+"<br>"+university;
			let today = new Date(); 
			document.getElementById("mydate").innerHTML=today.toISOString().split('T')[0]; 
		</script>
	</Layout></Slide>
	<!-- TOC -->
	<!--
	<Slide>
		<script>
			toc=true; // decides whether to generate table of content page
		</script>
		<Layout>
			<toc class="flex h-full items-center justify-center gap-[100px]">
				<chpicons> </chpicons>
				<chpnames class="text-left"> </chpnames>
			</toc>
		</Layout>
	</Slide>
	-->
	
	

	<!-- <script>newChapter("Greeting");</script> -->
	<!-- <script>newSection("Title");</script> -->
	<Slide animate><Layout>
		<titlebar> Suspects </titlebar>
		<mybody>
			<!-- <div data-id="header" class="text-center w-full h-full text-[60px] place-content-center flex items-center rounded gap-4 p-4">
				<p data-id="header-text" class="text-[60px]">ChameleonMT</p>
				<Media data-id="header-logo" class="object-contain h-[80px] w-[30%]" src="project_logo.png" type="img"/>
				<p data-id="header-text" class="text-[60px]">Master Thesis</p>
			</div> -->
	
			<!-- <div data-id="header-bot" class="text-center h-full w-full place-content-center flex items-center rounded gap-4 pg-2 p-4 bg-gray-600">
				<FitText>Neural Machine Translation for Low-Resource Language Variations <br> on Synthetic Data by Incorporating Linguistic Information</FitText>
			</div> -->
			<div class="grid" style="grid-template-columns: auto auto auto auto; mx-auto my-auto;">
				
				<!-- Names -->
				<div class="flex w-[25vw] items-center justify-center gap-[10px]">
					Christian Schuler <br> (Student)
				</div>
				<div class="flex w-[25vw] items-center justify-center gap-[10px]">
					Dr. Sina Ahmadi <br> (Supervisor)
				</div>
				<div class="flex w-[25vw] items-center justify-center gap-[10px]">
					Dr. Seid Muhie Yimam <br> (Supervisor & Examiner)
				</div>
				<div class="flex w-[25vw] items-center justify-center gap-[10px]">
					Prof. Dr. Chris Biemann <br> (Examiner)
				</div>

				<!-- Images -->
				<figure class="h-[60vh] w-[20vw] float-left mx-auto my-auto">
					<a href="https://christianschuler8989.github.io/">
						<img src="student_christian.jpg" alt="christian" class="h-[40vh]">
						<figcaption class="text-[2.3vh]">
							Master student in computer science at University of Hamburg.
						</figcaption>
						<figcaption class="text-[1.3vh]">
							With a passion for languages and colors, he aims to do a PhD. <br>Additionally, he eats more pizza in one year than any of you in your lifetime!
						</figcaption>
					</a>
				</figure>
				
				<figure class="h-[60vh] w-[20vw] float-left mx-auto my-auto">
					<a href="https://sinaahmadi.github.io/">
						<img src="supervisor_sina.png" alt="sina" class="h-[40vh]">
					</a>
					<figcaption class="text-[2.3vh]">
						Postdoctoral researcher affiliated with Prof. Rico Sennrich’s group at the Department of Computational Linguistics at University of Zurich. 
					</figcaption>
					<figcaption class="text-[1.3vh]">
						Sina always made sure to bring me back on track when I got too interested in side projects and literature!
					</figcaption>
				</figure>
				<figure class="h-[60vh] w-[20vw] float-left mx-auto my-auto">
					<a href="https://seyyaw.github.io/">
						<img src="supervisor_seid.jpeg" alt="seid" class="h-[40vh]">
					</a>
					<figcaption class="text-[2.3vh]">
						Technical Lead at HCDS and Research Associate at Language Technology Group, under the supervision of Prof. Chris Biemann.
					</figcaption>
					<figcaption class="text-[1.3vh]">
						Seid always kept a positive spirit and turned into an accomplice for some of the interesting side projects!
					</figcaption>
				</figure>
				<figure class="h-[60vh] w-[20vw] float-left mx-auto my-auto">
					<a href="https://www.inf.uni-hamburg.de/en/inst/ab/lt/people/chris-biemann.html">
						<img src="examiner_chris.jpg" alt="chris" class="h-[40vh]">
					</a>
					<figcaption class="text-[2.3vh]">
						Head of the Language Technology group at Universität Hamburg. 
					</figcaption>
					<figcaption class="text-[1.3vh]">
						Chris is the best lazerkasoo player I have ever heard of!
					</figcaption>
				</figure>

				<!-- Logos -->
				<figure class="flex h-[15vh] w-[25vw] items-center justify-center mx-auto my-auto">
					<img src="up-uhh-logo-u-2010-u-png.png" alt="uhh-logo" class="h-[15vh]">
				</figure>
				<!-- <div class="grid" style="grid-template-columns: auto; mx-auto my-auto;"> -->
				<figure class="flex h-[15vh] w-[25vw] items-center justify-center mx-auto my-auto">
					<img src="Logo_university-of-zurich-eth-zurich-biointerfaces-international-2018-zurich-lucerne-university-of-applied-sciences-and-arts-others.png" alt="uhh-logo" class="h-[7vh]">
				<!-- </figure> -->
				<!-- <figure class="flex h-[10vh] w-[15vw] items-center justify-center mx-auto my-auto"> -->
					<img src="Logo_George-Mason-University-2024_0.png" alt="uhh-logo" class="h-[15vh]">
				</figure>
				<!-- </div> -->
				
				<figure class="flex h-[15vh] w-[25vw] items-center justify-center mx-auto my-auto">
					<img src="up-uhh-logo-u-2010-u-png.png" alt="uhh-logo" class="h-[15vh]">
				</figure>
				<figure class="flex h-[15vh] w-[25vw] items-center justify-center mx-auto my-auto">
					<img src="up-uhh-logo-u-2010-u-png.png" alt="tum-logo" class="h-[15vh]">
				</figure>

			</div>
		</mybody>

		<Notes>
			I am Christian, and this is my Master Thesis: ChameleonMT :D
		</Notes>
	</Layout></Slide>

	
	<script>newChapter("Introduction");</script>
	<!-- <script>newSection("Motivation");</script> -->
	<Slide><Layout>
		<titlebar> Motivation </titlebar>
		<mybody>
			<div class="flex h-full items-center justify-center gap-[100px]">
				Placeholder
			</div>
		</mybody>
	</Layout></Slide>

	<!-- <script>newSection("Problem");</script> -->
	<Slide><Layout>
		<titlebar> Problem </titlebar>
		<mybody>
			<div class="flex h-full items-center justify-center gap-[100px]">
				Placeholder
			</div>
		</mybody>
	</Layout></Slide>

	<!-- <script>newSection("Hypothesis");</script> -->
	<Slide><Layout>
		<titlebar> Hypothesis </titlebar>
		<mybody>
			<div class="flex h-full items-center justify-center gap-[100px]">
				Placeholder
			</div>
		</mybody>
	</Layout></Slide>

	<!-- <script>newSection("Research Questions");</script> -->
	<Slide><Layout>
		<titlebar> Research Questions </titlebar>
		<mybody>
			<div class="flex h-full items-center justify-center gap-[100px]">
				Placeholder
			</div>
		</mybody>
	</Layout></Slide>


	<script>newChapter("Theory");</script>
	<!-- <script>newSection("Related Work");</script> -->
	<Slide><Layout>
		<titlebar> Related Work </titlebar>
		<mybody>
			<div class="flex h-full items-center justify-center gap-[100px]">
				Placeholder
			</div>
		</mybody>
	</Layout></Slide>

	<!-- <script>newSection("Synthetic Data");</script> -->
	<Slide animate><Layout>
		<titlebar> Synthetic Data </titlebar>
		<mybody>
			<div class="w-[95vw] h-[75vh] bg-gray-700"> <!-- Main Panel Bottom-->
				<iframe src="pdf/ChameleonMT-Concept-Dual.pdf#page=1&zoom=200" frameBorder="0" scrolling="auto" height="100%" width="100%" title="Documentation"></iframe>
			</div>
		</mybody>
	</Layout></Slide>

	<!-- <script>newSection("State of the Art");</script> -->
	<Slide><Layout>
		<titlebar> State of the Art </titlebar>
		<mybody>
			<div class="flex h-full items-center justify-center gap-[100px]">
				Placeholder
			</div>
		</mybody>
	</Layout></Slide>


	<script>newChapter("Methodology");</script>
	<!-- <script>newSection("Machine Translation");</script> -->
	<Slide><Layout>
		<titlebar> Machine Translation </titlebar>
		<mybody>
			<div class="flex h-full items-center justify-center gap-[100px]">
				Placeholder
			</div>
		</mybody>
	</Layout></Slide>


	<script>newChapter("Exploration");</script>
	<!-- <script>newSection("Bilingual Lexicon Induction");</script> -->
	<Slide><Layout>
		<titlebar> MUSE </titlebar>
		<mybody>
			<div class="flex h-full items-center justify-center gap-[100px]">
				Placeholder
			</div>
		</mybody>
	</Layout></Slide>

	<Slide><Layout>
		<titlebar> MUSE Issues </titlebar>
		<mybody>
			<div class="grid mt-[10vh] mx-[10vh]" style="grid-template-columns: auto;">
				<p>
					I found an issue on github that described my problem and a possible solution, but alas...
				</p>
				
				<figure>
					<img src="images/MUSE-github-issue-sina.png" alt="museissue" class="mx-auto my-[2vh]">
					<figcaption> MUSE GitHub Issue #196: https://github.com/facebookresearch/MUSE/issues/196</figcaption>
				</figure>
			</div>
		</mybody>
	</Layout></Slide>

	

	<!-- <script>newSection("Phase 2");</script> -->
	<Slide><Layout>
		<titlebar> Phase 2 </titlebar>
		<mybody>
			<div class="flex h-full items-center justify-center gap-[100px]">
				Placeholder
			</div>
		</mybody>
	</Layout></Slide>

	
	<script>newChapter("Design");</script>
	<!-- <script>newSection("Phase 1");</script> -->
	<Slide><Layout>
		<titlebar> Phase 1 </titlebar>
		<mybody>
			<div class="flex h-full items-center justify-center gap-[100px]">
				Placeholder
			</div>
		</mybody>
	</Layout></Slide>

	<!-- <script>newSection("Phase 2");</script> -->
	<Slide><Layout>
		<titlebar> Phase 2 </titlebar>
		<mybody>
			<div class="flex h-full items-center justify-center gap-[100px]">
				Placeholder
			</div>
		</mybody>
	</Layout></Slide>


	<script>newChapter("Development");</script>
	<!-- <script>newSection("Phase 1");</script> -->
	<Slide><Layout>
		<titlebar> Phase 1 </titlebar>
		<mybody>
			<div class="flex h-full items-center justify-center gap-[100px]">
				Placeholder
			</div>
		</mybody>
	</Layout></Slide>

	<!-- <script>newSection("Phase 2");</script> -->
	<Slide><Layout>
		<titlebar> Phase 2 </titlebar>
		<mybody>
			<div class="flex h-full items-center justify-center gap-[100px]">
				Placeholder
			</div>
		</mybody>
	</Layout></Slide>


	<script>newChapter("Data");</script>
	<!-- <script>newSection("Data Acquisition");</script> -->
	<Slide><Layout>
		<titlebar> Data Acquisition</titlebar>
		<mybody>
			<div class="flex h-full items-center justify-center gap-[100px]">
				Placeholder
			</div>
		</mybody>
	</Layout></Slide>

	<!-- <script>newSection("Data Cleaning");</script> -->
	<Slide><Layout>
		<titlebar> Data Cleaning</titlebar>
		<mybody>
			<div class="flex h-full items-center justify-center gap-[100px]">
				Placeholder
			</div>
		</mybody>
	</Layout></Slide>

	<!-- <script>newSection("Part 1");</script> -->
	<Slide><Layout>
		<titlebar> Part 3 </titlebar>
		<mybody>
			<div class="flex h-full items-center justify-center gap-[100px]">
				Placeholder
			</div>
		</mybody>
	</Layout></Slide>

	<!-- <script>newSection("Part 2");</script> -->
	<Slide><Layout>
		<titlebar> Part 4 </titlebar>
		<mybody>
			<div class="flex h-full items-center justify-center gap-[100px]">
				Placeholder
			</div>
		</mybody>
	</Layout></Slide>


	<script>newChapter("Experiments");</script>
	<!-- <script>newSection("Experiment A");</script> -->
	<Slide><Layout>
		<titlebar> Experiment A </titlebar>
		<mybody>
			<div class="flex h-full items-center justify-center gap-[100px]">
				Placeholder
			</div>
		</mybody>
	</Layout></Slide>

	<!-- <script>newSection("Experiment B");</script> -->
	<Slide><Layout>
		<titlebar> Experiment B </titlebar>
		<mybody>
			<div class="flex h-full items-center justify-center gap-[100px]">
				Placeholder
			</div>
		</mybody>
	</Layout></Slide>


	<script>newChapter("Results");</script>
	<!-- <script>newSection("Part 1");</script> -->
	<Slide><Layout>
		<titlebar> Part 1 </titlebar>
		<mybody>
			<div class="flex h-full items-center justify-center gap-[100px]">
				Placeholder
			</div>
		</mybody>
	</Layout></Slide>

	<!-- <script>newSection("Part 2");</script> -->
	<Slide><Layout>
		<titlebar> Part 2 </titlebar>
		<mybody>
			<div class="flex h-full items-center justify-center gap-[100px]">
				Placeholder
			</div>
		</mybody>
	</Layout></Slide>


	<script>newChapter("Discussion");</script>
	<!-- <script>newSection("Part 1");</script> -->
	<Slide><Layout>
		<titlebar> Part 1 </titlebar>
		<mybody>
			<div class="flex h-full items-center justify-center gap-[100px]">
				Placeholder
			</div>
		</mybody>
	</Layout></Slide>

	<!-- <script>newSection("Part 2");</script> -->
	<Slide><Layout>
		<titlebar> Part 2 </titlebar>
		<mybody>
			<div class="flex h-full items-center justify-center gap-[100px]">
				Placeholder
			</div>
		</mybody>
	</Layout></Slide>


	<script>newChapter("Future Work");</script>
	<!-- <script>newSection("Direction A");</script> -->
	<Slide><Layout>
		<titlebar> Direction A </titlebar>
		<mybody>
			<div class="flex h-full items-center justify-center gap-[100px]">
				Placeholder
			</div>
		</mybody>
	</Layout></Slide>

	<!-- <script>newSection("Direction B");</script> -->
	<Slide><Layout>
		<titlebar> Direction B</titlebar>
		<mybody>
			<div class="flex h-full items-center justify-center gap-[100px]">
				Placeholder
			</div>
		</mybody>
	</Layout></Slide>


	<script>newChapter("Conclusion");</script>
	<!-- <script>newSection("Regarding RQ-1");</script> -->
	<Slide><Layout>
		<titlebar> Regarding RQ-1 </titlebar>
		<mybody>
			<div class="flex h-full items-center justify-center gap-[100px]">
				Placeholder
			</div>
		</mybody>
	</Layout></Slide>

	<!-- <script>newSection("Regarding RQ-2");</script> -->
	<Slide><Layout>
		<titlebar> Regarding RQ-2 </titlebar>
		<mybody>
			<div class="flex h-full items-center justify-center gap-[100px]">
				Placeholder
			</div>
		</mybody>
	</Layout></Slide>


	<script>newChapter("Appendix");</script>
	<!-- <script>newSection("Appendix A");</script> -->
	<Slide><Layout>
		<titlebar> Appendix A </titlebar>
		<mybody>
			<div class="flex h-full items-center justify-center gap-[100px]">
				Placeholder
			</div>
		</mybody>
	</Layout></Slide>

	<!-- <script>newSection("Appendix B");</script> -->
	<Slide><Layout>
		<titlebar> Appendix B </titlebar>
		<mybody>
			<div class="flex h-full items-center justify-center gap-[100px]">
				Placeholder
			</div>
		</mybody>
	</Layout></Slide>

	<!---
	- Put Pizza-Statistics into Appendix
	
	-->




	<!-- to mimic the latex template  -->
	<script>
		const totalSlides = document.getElementsByTagName('pagenumber').length;
		const totalChapters = chapterNames.length;
		var temp; 
		for (let i = 0; i < totalSlides; i++) {
			// one section, one slide
			document.getElementsByTagName('section')[i].setAttribute("id", "slide-"+(i+1));
			// add author name 
			document.getElementsByTagName('author')[i].innerText=authorshort;
			// add title 
			document.getElementsByTagName('mytitle')[i].innerHTML="<a href=\"#slide-1\">"+title+"</a>";
			// show slide number with total slide number
			document.getElementsByTagName("pagenumber")[i].innerHTML = (i+1)+"/"+totalSlides;
		}
		for (let i = 0; i < totalSlides; i++) {
			for (let j = 0; j < totalChapters; j++) {
				// fill in chapter names
				temp = document.querySelectorAll("table.topbar")[i]; 
				temp.getElementsByTagName("tr")[0].innerHTML += "<th data-chpcol=\"chpcol\" style=\"font-weight:normal\">"+chapterNames[j]+"</th>";
				// document.getElementsByTagName("test")[0].innerHTML="here!"; 
				// fill in dots
				let slidesInChapter = presentationData.filter(item => item.chapter == chapterNames[j]);
				let begin = slidesInChapter[0].pagenr;
				let end = slidesInChapter[slidesInChapter.length-1].pagenr;
				let circles=toCircle(begin,end);
				temp.getElementsByTagName("tr")[1].innerHTML += "<td>"+ circles +"</td>";
			}
		}
		for (let i = 0; i < totalSlides; i++) {
			// first, find out if title page and toc exist 
			let chapter0 = presentationData.filter(item => item.chapternr == 0).length;
			if (i>=chapter0){
				// then set corresponding circle to white
				let circle = document.getElementsByTagName("circle-"+(i+1))[i]; 
				circle.style.background="white";
				circle.style.border="0px";
				// also the chapter names 
				let chapterNr = presentationData.filter(item => item.pagenr == i+1)[0].chapternr;
				temp = document.getElementsByTagName("th")[(i)*(totalChapters)+chapterNr-1];
				if (temp.hasAttribute("data-chpcol")){ 
					temp.style.color="white";
				}
			}
		}
		// circles: start, start+1, . . . , end are created
		function toCircle(begin,end){
			let circles = ""; 
			for (let i=begin; i<=end; i++){
				circles+="<a href=\"#slide-" +i+ "\"><circle-" +i+ " class=\"dot\"> </circle-" +i+ "> </a>" ;
			}
			return circles;
		}
		// to create table of contents
		if (toc) {
			for (i=1; i<=chapterNames.length;i++){
				document.getElementsByTagName('chpicons')[0].innerHTML += "<div class=\"chpicon\">"+i+"</div> <br>";
				document.getElementsByTagName('chpnames')[0].innerHTML += "<div>"+chapterNames[i-1]+"</div> <br>";
			}
		}
	</script>
	
	<style>
		.chpicon{
			color: white;
			width:180%;
			background: var(--themecolor);
		}
		.dot {
			height: 15px;
			width: 15px;
			background: rgba(0,0,0,0);
			border-radius: 50%;
			border: 1.5px solid var(--themecolorlight);
			display: inline-block;
		}
		ul.a {
			list-style-type: square;
			padding-top:5vh;
		}
		ul.b {
			list-style-type: circle;
			margin-left:5vh;
			margin-right:5vh;
			padding-top:1vh;
			padding-bottom:1vh;
		}
		ul.c {
			list-style-type: disc;
			margin-left:10vh;
			margin-right:5vh;
			padding-top:1vh;
			padding-bottom:1vh;
		}
		ul{
			text-align: left;
			margin-left:20vh;
			margin-right:5vh;
			padding-top:1vh;
			padding-bottom:1vh;
		}
		titlebar{
			display: flex;
			background: rgb(242,242,242); 
			width: 100vw; 
			height: 9vh; 
			text-align: left;
			padding-left: 5vh; 
			padding-top: 2vh;
			font-size: 5vh;
		}
		mybody{
			display: flex;
			justify-content: center;
			align-items: center;
			height:79vh;
		}
		figure {
			border: 0px #cccccc solid;
			padding: 4px;
			margin: auto;
		}
		figcaption {
			background-color: rgb(242,242,242);
			color: black;
			font-style: italic;
			padding: 2px;
			text-align: center;
		}
	</style>
</Presentation>
