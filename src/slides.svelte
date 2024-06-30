<script lang="ts">
	import { Presentation, Slide, Media, FitText, Step, Stack, Code, Notes } from '@components'
	import Layout from './layout.svelte'
</script>

<!-- 
	Project Information #######################################################

	- MA-Thesis-Slides github repository: https://github.com/christianschuler8989/MA-Thesis-Slides
	- MA-Thesis-Slides online: https://christianschuler8989.github.io/MA-Thesis-Slides/#/slide-1
	- AwesomeAnranAnimotion: https://github.com/AnranW/AwesomeAnranAnimotion

	
	Typical Errors ############################################################

	→ pnpm run dev		NOT "pnpm dev run" . . . .
	
	"Uncaught TypeError: slidesInChapter[0] is undefined" and layout elements missing.
	→ This can happen if a chapter is defined but has no slides.

-->

<Presentation>	
	<script>
		// information about this presentation 
		const author = "Christian Schuler"; 
		const authorshort = "Schuler"; 
		const title = "Neural Machine Translation for Low-Resource Language Variations on Synthetic Data by Incorporating Linguistic Information";
		//             Neural Machine Translation for Low-Resource Language Variations on Synthetic Data by Incorporating Linguistic Information
		//             Leveraging Morphological and Lexical Features in Synthetic Data Generation for Dialect-Specific Machine Translation
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
		<titlebar> The Unusual Suspects </titlebar>
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
						<img src="examiner_chris.jpg" alt="chris" class="h-[40vh] mx-auto" >
					</a>
					<figcaption class="text-[2.3vh]">
						Head of the Language Technology group at Universität Hamburg. 
					</figcaption>
					<figcaption class="text-[1.3vh]">
						Chris is the best lazerkasoo player I have ever heard of!
					</figcaption>
				</figure>

			</div>
		</mybody>

		<Notes>
			I am Christian, and this is my Master Thesis: ChameleonMT :D
		</Notes>
	</Layout></Slide>

	
	<script>newChapter("Introduction");</script>
	<!-- <script>newSection("Motivation");</script> -->
	<!-- <Slide><Layout>
		<titlebar> Motivation </titlebar>
		<mybody>
			<div class="flex h-full items-center justify-center gap-[100px]">
				Placeholder
			</div>
		</mybody>
	</Layout></Slide> -->

	<!-- <Slide><Layout>
		<titlebar > Distribution of Languages on the Internet </titlebar>
		<mybody>
			<div class="flex items-center justify-center">
				<img class="h-[75vh] align-middle" src="LowResource-IL08.png" alt="weblanguages">
			</div>
		</mybody>
	</Layout></Slide> -->

	<!-- Not English = Low-Resource? -->
	<Slide><Layout>
		<titlebar > Distribution of Languages on the Internet </titlebar> 
		<mybody>
			<div class="flex items-center justify-center w-[50%] h-[100%]">
				<figure class="mx-auto my-auto" >
					<!-- <a href="URL_HERE"> -->
						<img class="align-middle" src="LowResource-IL09.png" alt="weblanguages">
					<!-- </a> -->
					<figcaption class="text-[2.3vh]">
						Distribution of Languages on the Internet.
					<div class="text-[2.1vh]">
						<br> (Source: https://en.wikipedia.org/wiki/Languages_used_on_the_Internet)
					</div>
					</figcaption>
				</figure>
			</div>

			<div class="flex items-center justify-center w-[50%] h-[100%]">
				<figure class="mx-auto my-auto" >
					<!-- <a href="URL_HERE"> -->
						<img src="LowResource-ResourceHierarchyZero.png" alt="bli" style="max-height:100%;">
					<!-- </a> -->
					<figcaption class="text-[3.3vh]">
						Low-Resource Language Processing.
					<div class="text-[2.1vh]">
						<br> (Modified from https://www.ruder.io/unsupervised-cross-lingual-learning/)
					</div>
					</figcaption>
				</figure>
			</div>
		</mybody>
	</Layout></Slide>

	<Slide><Layout>
		<titlebar > Guiding Questions </titlebar>
		<mybody>
			<div class="flex items-center justify-center">
				<ul class="a" >
					<li>(1.) What is the performance of the current state-of-the-art models in translating dialects?</li>
					<br>
					<li>(2.) Can we incorporate linguistic information in MT to synthetically generate sentences in language variants so that dialects of various (and especially low-resource) languages can be processed more efficiently?</li>
					<br>
					<li>(3.) When using synthetic data, what roles do state-of-the-art approaches in fine-tuning, transfer learning and adapters play in improving the performance of MT systems to process (particularly low-resource) language variations effectively?</li>
					<br>
					<li>(4.) What are requirements for deriving tools and processes that can be applied to vastly different languages from various language families?</li>
				</ul>
			</div>
		</mybody>
	</Layout></Slide>
	
	<Slide><Layout>
		<titlebar > Exploring Dialect Machine Translation </titlebar>
		<mybody>
			<div class="flex items-center justify-center">
				<figure class="mx-auto my-auto" >
					<img src="exploratory-2023_11_28-benglai.png" alt="exploringDialectMT">
				</figure>
			</div>
		</mybody>
	</Layout></Slide>

	<Slide><Layout>
		<titlebar > Exploring Dialect Machine Translation </titlebar>
		<mybody>
			<div class="grid" style="grid-template-columns: auto auto auto; mx-auto my-auto;">
				<!-- <figure class="mx-auto my-auto h-[85%] w-[85%]" >
					<img src="exploratory-2023_11_28-benglai.png" alt="exploringDialectMT">
				</figure> -->
				TODO: dd sources for models and text data
				<figure class="mx-auto my-auto h-[85%] w-[85%]" >
					<img src="exploratory-2023_11_28-centralKurdish.png" alt="exploringDialectMT">
				</figure>

				<figure class="mx-auto my-auto h-[85%] w-[85%]" >
					<img src="exploratory-2023_11_28-tigrinya.png" alt="exploringDialectMT">
				</figure>

				<figure class="mx-auto my-auto h-[85%] w-[85%]" >
					<img src="exploratory-2023_11_28-german.png" alt="exploringDialectMT">
				</figure>
			</div>
			<!-- <div class="flex items-center justify-center h-[90%]">
				<figure class="mx-auto my-auto h-[100%] w-[100%]" >
					<img src="images/german-dialects.png" alt="datacleaning" style="max-height:100%; max-width:100%;">
				<figcaption class="text-[1.8vh]">
					(Sima Brankov, 2013) Linguistic Map of Germany.
					<div class="text-[1.1vh]">
						<br> (Source: https://www.thegermanz.com/german-accents-dialects-german-germans-dont-understand/)
					</div>
				</figcaption>
				</figure>
			</div>

			<div class="flex items-center justify-center h-[90%]">
				<figure class="mx-auto my-auto h-[100%] w-[100%]" >
					<img src="images/allemagne201.png" alt="datacleaning" style="max-height:100%; max-width:100%;">
				<figcaption class="text-[1.8vh]">
					(Sima Brankov, 2016) Linguistic Map of Germany.
					<div class="text-[1.1vh]">
						<br> (Source: https://sblanguagemaps.wordpress.com/2016/06/12/linguistic-map-of-germany/)
					</div>
				</figcaption>
				</figure>
			</div> -->
		</mybody>
	</Layout></Slide>

	<script>newChapter("Language");</script>

	<Slide><Layout>
		<titlebar > German </titlebar>
		<mybody>
			<div class="flex items-center justify-center">
				<figure class="mx-auto my-auto h-[100%] w-[100%]" >
					<a href="https://github.com/facebookresearch/fairseq/tree/nllb">
						<img src="ChameleonMT-MT-NLLB-German.png" alt="performanceOfMTSystems" style="max-height:100%; max-width:100%;">
					</a>
				<figcaption class="text-[1.8vh]">
					(NLLB Team et al., 2022) open-sourced models capable of high-quality translations between 200+ languages. 
					<br> Any following mention of NLLB refers to the 3.3B model.
				</figcaption>
				</figure>
			</div>
		</mybody>
	</Layout></Slide>

	<Slide><Layout>
		<titlebar > German == German ? </titlebar>
		<mybody>
			<figure>
				<video controls class="w-[80%] mx-auto my-auto p-2">
					<source src="/video/german_dialects.mp4" type="video/mp4" />
					<track kind="captions" label="English" srclang="eng" src="media-video-captions-eng.vtt"/>
					<track kind="captions" label="German" srclang="deu" src="media-video-captions-deu.vtt" default/>
				</video>
				<figcaption class="text-[1.8vh]"> 
					Peter Frankenfeld - Die Wetterkarte - Deutsche Dialekte 	
				<div class="text-[1.1vh]">
					<br> (Source: https://www.youtube.com/watch?v=btlGMBA2XO4)
				</div>
				</figcaption>
			</figure>
		</mybody>
	</Layout></Slide>

	<Slide><Layout>
		<titlebar > German </titlebar>
		<mybody>
			<div class="flex items-center justify-center h-[90%]">
				<figure class="mx-auto my-auto h-[100%] w-[100%]" >
					<img src="images/german-dialects.png" alt="datacleaning" style="max-height:100%; max-width:100%;">
				<figcaption class="text-[1.8vh]">
					(Sima Brankov, 2013) Linguistic Map of Germany.
					<div class="text-[1.1vh]">
						<br> (Source: https://www.thegermanz.com/german-accents-dialects-german-germans-dont-understand/)
					</div>
				</figcaption>
				</figure>
			</div>

			<div class="flex items-center justify-center h-[90%]">
				<figure class="mx-auto my-auto h-[100%] w-[100%]" >
					<img src="images/allemagne201.png" alt="datacleaning" style="max-height:100%; max-width:100%;">
				<figcaption class="text-[1.8vh]">
					(Sima Brankov, 2016) Linguistic Map of Germany.
					<div class="text-[1.1vh]">
						<br> (Source: https://sblanguagemaps.wordpress.com/2016/06/12/linguistic-map-of-germany/)
					</div>
				</figcaption>
				</figure>
			</div>
		</mybody>
	</Layout></Slide>

	
	<Slide><Layout>
		<titlebar > German as Dialect Continuum </titlebar>
		<mybody>
			<div class="flex items-center justify-center h-[90%]">
				<figure class="mx-auto my-auto h-[100%] w-[100%]" >
					<img src="images/Lameli_2008_German_Dialect_Continuum_Map.png" alt="datacleaning" style="max-height:100%; max-width:100%;">
				<figcaption class="text-[1.8vh]">
					(Lameli, 2008) investigated local variants of German.
					<div class="text-[1.1vh]">
						<br> (Source: https://aktuell.nationalatlas.de/wp-content/uploads/08_09_Dialektraeume.pdf)
					</div>
				</figcaption>
				</figure>
			</div>
		</mybody>
	</Layout></Slide>

	<Slide><Layout>
		<titlebar > German as Dialect Continuum </titlebar>
		<mybody>
			<div class="flex items-center justify-center h-[90%]">
				<figure class="mx-auto my-auto h-[100%] w-[100%]" >
					<img src="images/Lameli_2008_German_Dialect_Continuum_Table.png" alt="datacleaning" style="max-height:100%; max-width:100%;">
				<figcaption class="text-[1.8vh]">
					(Lameli, 2008) displays the phonetic changes across German-speaking regions.
					<div class="text-[1.1vh]">
						<br> (Source: https://aktuell.nationalatlas.de/wp-content/uploads/08_09_Dialektraeume.pdf)
					</div>
				</figcaption>
				</figure>
			</div>
		</mybody>
	</Layout></Slide>

	<script>newChapter("Methods & Experiments");</script>

	<Slide><Layout>
		<titlebar > Linguistic Features </titlebar>
		<mybody>
			<div class="flex items-center justify-center">
				<figure class="mx-auto my-auto h-[100%] w-[100%]" >
					<img src="images/FILE_HERE" alt="datacleaning" style="max-height:100%; max-width:100%;">
				<figcaption class="text-[1.8vh]">
					Text:
					<br> Text.
				</figcaption>
				</figure>
			</div>
		</mybody>
	</Layout></Slide>

	<Slide><Layout>
		<titlebar > Bilingual Lexicon Induction </titlebar>
		<mybody>
			<div class="flex items-center justify-center">
				<figure class="mx-auto my-auto h-[100%] w-[100%]" >
					<img src="ChameleonMT-BLI-BLI.png" alt="bli" style="max-height:100%; max-width:100%;">
				<figcaption class="text-[1.8vh]">
					Inspiration for this figure:
					<br> (Wang et al., 2021) Porject Report - Training Domain Specific Multilingually Aligned Word Embeddings
					<br> (Irvine and Callison-Burch, 2017) A Comprehensive Analysis of Bilingual Lexicon Induction
				</figcaption>
				</figure>
			</div>
		</mybody>
	</Layout></Slide>

	

	<Slide><Layout>
		<titlebar > Synthetic Data </titlebar>
		<mybody>
			<div class="flex items-center justify-center">
				<figure class="mx-auto my-auto h-[100%] w-[100%]" >
					<img src="images/FILE_HERE" alt="datacleaning" style="max-height:100%; max-width:100%;">
				<figcaption class="text-[1.8vh]">
					Text:
					<br> Text.
				</figcaption>
				</figure>
			</div>
		</mybody>
	</Layout></Slide>

	<Slide><Layout>
		<titlebar > Evaluation Metrics </titlebar>
		<mybody>
			<div class="flex items-center justify-center">
				<figure class="mx-auto my-auto h-[100%] w-[100%]" >
					<img src="images/FILE_HERE" alt="datacleaning" style="max-height:100%; max-width:100%;">
				<figcaption class="text-[1.8vh]">
					Text:
					<br> Text.
				</figcaption>
				</figure>
			</div>
		</mybody>
	</Layout></Slide>

	<Slide><Layout>
		<titlebar > Data Cleaning </titlebar>
		<mybody>
			<div class="flex items-center justify-center h-[100%]">
				<figure class="mx-auto my-auto h-[100%]" >
					<!-- <a href="URL_HERE"> -->
						<img src="ChameleonMT-DATA-DialectBLI02.png" alt="datacleaning" style="max-height:100%;">
					<!-- </a> -->
					<figcaption class="text-[2.3vh]">
						Examples of "aligned" Bavarian and Standard German sentences that have been excluded from the dataset 
						<br> (smaller font indicates content missing in the other variant's sentence)

					</figcaption>
				</figure>
			</div>
		</mybody>
	</Layout></Slide>

	<script>newChapter("Results");</script>
	<Slide><Layout>
		<titlebar > What I got out of it</titlebar>
		<mybody>
			<div class="flex items-center justify-center">
				<figure class="mx-auto my-auto h-[100%] w-[100%]" >
					<img src="images/MA-Data-Maps-20240627135334614.webp" alt="datacleaning" style="max-height:100%; max-width:100%;">
				<figcaption class="text-[1.8vh]">
					(Burghardt et al., 2016) created (but did not release) a lexicon of Bavarian dialects.
					<br> Overview of the main Bavarian dialect families and the regions where they occur.
				</figcaption>
				</figure>
			</div>
		</mybody>
	</Layout></Slide>


	<!-- <script>newChapter("Main Challenge");</script> -->
	<script>newChapter("Related Work");</script>
	<Slide><Layout>
		<titlebar > Origin of the Noise - Bavarian Dialect Families</titlebar>
		<mybody>
			<div class="flex items-center justify-center">
				<figure class="mx-auto my-auto h-[100%] w-[100%]" >
					<img src="images/MA-Data-Maps-20240627135334614.webp" alt="datacleaning" style="max-height:100%; max-width:100%;">
				<figcaption class="text-[1.8vh]">
					(Burghardt et al., 2016) created (but did not release) a lexicon of Bavarian dialects.
					<br> Overview of the main Bavarian dialect families and the regions where they occur.
				</figcaption>
				</figure>
			</div>
		</mybody>
	</Layout></Slide>

	<Slide><Layout>
		<titlebar > Origin of the Noise - Bavarian Varieties</titlebar>
		<mybody>
			<div class="flex items-center justify-center">
				<figure class="mx-auto my-auto h-[100%] w-[100%]" >
					<img src="images/MA-Data-Maps-20240630123335540.webp" alt="datacleaning" style="max-height:100%; max-width:100%;">
				<figcaption class="text-[1.8vh]">
					German-Wikipedia article for Bairisch (https://de.wikipedia.org/wiki/Bairisch) regarding Middle-Bavarian variants: 
					<br> 
					<br> Die Tabelle ist dabei stark vereinfacht. In der westlichen Variante wird häufig noch das „r“ gesprochen, 
					<br> das im Ostmittelbairischen und im Standarddeutschen gerne vokalisiert wird; also z. B. i får, hart, hårt, hirt. 
					<br> 
					<br> (Eng:) The table is very simplyfied. In the western variant the "r" is often times still spoken, 
					<br> while the eastern-middle variant and Standard German tend to vocalize it; meaning for example: i får, hart, hårt, hirt."
				</figcaption>
				</figure>					
			</div>
		</mybody>
	</Layout></Slide>

	<Slide><Layout>
		<titlebar > Origin of the Noise - Transition Zones</titlebar>
		<mybody>
			<div class="flex items-center justify-center h-[85%]">
				<figure class="mx-auto my-auto h-[100%] w-[100%]" >
					<!-- <a href="URL_HERE"> -->
						<img src="images/MA-Data-Maps-20240627134952078.webp" alt="datacleaning" style="max-height:100%;">
					<!-- </a> -->
					<figcaption class="text-[1.8vh]">
						(Lanwermeyer et al., 2016) investigate how dialect variation influences phonological and lexical-semantic word processing:
						<br> The Bavarian-Alemannic transition zone (BA) and the Central Bavarian dialect area (CB) 
						<br> with × displaying the recording location (Merching) and experimentation location (Isen).
					</figcaption>
				</figure>
			</div>
		</mybody>
	</Layout></Slide>
	
	<Slide><Layout>
		<titlebar > Origin of the Noise - Alpine Region</titlebar>
		<mybody>
			<div class="flex items-center justify-center h-[90%]">
				<figure class="mx-auto my-auto h-[95%]" >
					<!-- <a href="URL_HERE"> -->
						<img src="images/MA-Data-Maps-20240627132734017.webp" alt="datacleaning" style="max-height:100%;">
					<!-- </a> -->
					<figcaption class="text-[1.8vh]">
						(Vergeiner and Bülow, 2023) investigate geolinguistic structures of dialect phonology in German-speaking Alpine regions:
						<br> Bavarian and Alemannic dialects according to Wiesinger (1983) (the chequered areas are transition zones, the red line marks the borders of the Alpine region according to the Alpine Convention; 
						<br> for further information on the Alpine Convention, see https://www.alpconv.org/en/home/convention/).
					</figcaption>
				</figure>
			</div>
		</mybody>
	</Layout></Slide>


	<Slide><Layout>
		<titlebar > Origin of the Noise - Bavarian(s)</titlebar>
		<mybody>
			<div class="flex items-center justify-center">
				<figure class="mx-auto my-auto h-[90%]" >
					<a href="https://github.com/UniversalDependencies/UD_Bavarian-MaiBaam">
						<img src="images/German-Varieties-20240405134346025.webp" alt="datacleaning" style="max-height:100%;">
					</a> 
					<figcaption class="text-[1.8vh]">
						In May (Blaschke et al., 2024) released a multi-dialectal Bavarian Universal Dependency treebank
						<br> with manually annotated part-of-speech tags and syntactic dependencies:
						<br> Bavarian dialect groups in Germany, Austria and Italy, based on the classification by Wiesinger (1983, map 47.4).
						<br> Names of dialect groups are in small caps, names of provinces and states in italics.
					</figcaption>
				</figure>
			</div>
		</mybody>
	</Layout></Slide>
	

	
	
	<script>newChapter("Next Steps");</script>

	<Slide><Layout>
		<titlebar > Sorting Wikipedia Articles - Alemannic Example </titlebar>
		<mybody>
			<div class="flex items-center justify-center h-[80%]">
				<figure class="mx-auto my-auto h-[100%] w-[100%]" >
					<img src="images/MA-Thesis-Alemannic-Lambrecht-Map.png" alt="alemannic_map" style="max-height:100%; max-width:100%;">
				<figcaption class="text-[1.8vh]">
					(Lambrecht et al., 2022) worked on Machine Translation from 
					<br> Standard German to Alemannic Dialects: 
					<br> Alemannic variants with fluent transitions.
					<div class="text-[0.7vh]">
						<br> (Source: https://sigul-2022.ilc.cnr.it/wp-content/uploads/2022/06/MT-from-Standard-German-to-Alemannic-Dialects-Louisa-Lambrecht-Felix-Schneider-Alexander-Waibel.pdf)
					</div>
				</figcaption>
				</figure>
			</div>
		</mybody>
	</Layout></Slide>

	<Slide><Layout>
		<titlebar > Sorting Wikipedia Articles - Alemannic Example </titlebar>
		<mybody>
			<div class="flex items-center justify-center">
				<figure class="mx-auto my-auto h-[100%] w-[100%]" >
					<img src="images/MA-Thesis-Alemannic-Lambrecht-Table.png" alt="alemannic_map" style="max-height:100%; max-width:100%;">
				<figcaption class="text-[1.8vh]">
					(Lambrecht et al., 2022): Splitting the Corpora via linguistic analysis.
					<div class="text-[0.7vh]">
						<br> (Source: https://sigul-2022.ilc.cnr.it/wp-content/uploads/2022/06/MT-from-Standard-German-to-Alemannic-Dialects-Louisa-Lambrecht-Felix-Schneider-Alexander-Waibel.pdf)
					</div>
				</figcaption>
				</figure>
			</div>
		</mybody>
	</Layout></Slide>

	<Slide><Layout>
		<titlebar > Sorting Wikipedia Articles - Alemannic Example </titlebar>
		<mybody>
			<div class="flex items-center justify-center">
				<figure class="mx-auto my-auto h-[100%] w-[100%]" >
					<img src="images/MA-Thesis-Alemannic-Lambrecht-Pie.png" alt="alemannic_map" style="max-height:100%; max-width:100%;">
				<figcaption class="text-[1.8vh]">
					(Lambrecht et al., 2022): Categorisation of Alemannic and Distribution of tagged articles.
						<br> Margravian (mg), Basel German (bd), Swabian (sw), High Alemannic (ha), 
						<br> Low Alemannic (na), Highest Alemannic (hoe), Alsatian (els), others (so).
					<div class="text-[0.7vh]">
						<br> (Source: https://sigul-2022.ilc.cnr.it/wp-content/uploads/2022/06/MT-from-Standard-German-to-Alemannic-Dialects-Louisa-Lambrecht-Felix-Schneider-Alexander-Waibel.pdf)
					</div>
				</figcaption>
				</figure>
			</div>
		</mybody>
	</Layout></Slide>

	<Slide><Layout>
		<titlebar > Wikidumps </titlebar>
		<mybody>
			<div class="flex items-center justify-center">
				<figure class="mx-auto my-auto h-[100%] w-[100%]" >
					<img src="ChameleonMT-DATA-WikidumpsProgress.png" alt="wikidumpprogress" style="max-height:100%; max-width:100%;">
				<figcaption class="text-[1.8vh]">
					Current progress of this approach (for Alemannic and Bavarian). 
				</figcaption>
				</figure>
			</div>
		</mybody>
	</Layout></Slide>



	<Slide><Layout>
		<titlebar > NLLB-Tuning </titlebar>
		<mybody>
			<div class="flex items-center justify-center">
				Once the quality of data cleaning and perturbation has reached the next step. 
			</div>
		</mybody>
	</Layout></Slide>

	<Slide><Layout>
		<titlebar > Beyond German - Northern Kurdish (Kurmanjî) and Central Kurdish (Soranî) </titlebar>
		<mybody>
			<div class="flex items-center justify-center">
				<ul class="a" >
					<li>OpusTools provides (somewhat) aligned data for both</li>
					<br>
					<li>Both have their own wikipedia <p class="text-[2.1vh]">(https://meta.wikimedia.org/wiki/List_of_Wikipedias)</p></li>
					<ul class="b"> 
						<li>English: 6,843,344</li>
						<li>German: 2,922,376</li>
						<li>Kurmanjî: 76,183</li>
						<li>Soranî: 56,007</li>
						<li>Alemannic: 30,509</li>
						<li>Bavarian: 27,168</li>
					</ul>
					<br>
					<li>Already got a small set of data filtered by sub-dialects</li>
				</ul>
			</div>
		</mybody>
	</Layout></Slide>

	<Slide><Layout>
		<titlebar > Clean Data - Better Alignments </titlebar>
		<mybody>
			<div class="flex items-center justify-center h-[90%]">
				<figure class="mx-auto my-auto h-[100%] w-[100%]" >
					<img src="LanguageData-TextAlignments.png" alt="wikidumpprogress" style="max-height:100%; max-width:100%;">
				<figcaption class="text-[1.8vh]">
					Notion to reduce noise in available (aligned) data sources via language models. 
				</figcaption>
				</figure>
			</div>
		</mybody>
	</Layout></Slide>





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
