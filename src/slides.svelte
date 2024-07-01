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
			<img class="h-[18vh] w-auto align-middle" src="up-uhh-logo-u-2010-u-png.png" alt="uhh logo">
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
			<div class="grid mx-auto my-auto" style="grid-template-columns: auto auto auto auto;">
				
				<!-- Names -->
				<div class="flex w-[25vw] items-center justify-center gap-[10px]">
					Christian Schuler <br> 
				</div>
				<div class="flex w-[25vw] items-center justify-center gap-[10px]">
					Dr. Sina Ahmadi <br> 
				</div>
				<div class="flex w-[25vw] items-center justify-center gap-[10px]">
					Dr. Seid Muhie Yimam <br> 
				</div>
				<div class="flex w-[25vw] items-center justify-center gap-[10px]">
					Prof. Dr. Chris Biemann <br> 
				</div>

				<!-- Images -->
				<figure class="h-[70vh] w-[24vw] float-left mx-auto my-auto">
					<a href="https://christianschuler8989.github.io/">
						<img src="christian_schuler_01.png" alt="christian" class="h-[60vh] mx-auto">
					</a>
					<figcaption class="text-[3.3vh]">
						(Student)
					</figcaption>
				</figure>

				<figure class="h-[70vh] w-[24vw] float-left mx-auto my-auto">
					<a href="https://sinaahmadi.github.io/">
						<img src="sina_ahmadi_05.png" alt="sina" class="h-[60vh] mx-auto">
					</a>
					<figcaption class="text-[3.3vh]">
						(Supervisor)
					</figcaption>
				</figure>

				<figure class="h-[70vh] w-[24vw] float-left mx-auto my-auto">
					<a href="https://seyyaw.github.io/">
						<img src="seid_muhie_yimam_05.png" alt="seid" class="h-[60vh] mx-auto">
					</a>
					<figcaption class="text-[3.3vh]">
						(Supervisor & Examiner)
					</figcaption>
				</figure>

				<figure class="h-[70vh] w-[24vw] float-left mx-auto my-auto">
					<a href="https://www.inf.uni-hamburg.de/en/inst/ab/lt/people/chris-biemann.html">
						<img src="chris_biemann_05.png" alt="chris" class="h-[60vh] mx-auto" >
					</a>
					<figcaption class="text-[3.3vh]">
						(Examiner)
					</figcaption>
				</figure>
				
				<!-- <figure class="h-[60vh] w-[20vw] float-left mx-auto my-auto">
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
				</figure> -->

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
			<div class="flex items-center justify-center w-[50%] h-[100%] ml-[-3%]">
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
					<li class="text-[5.1vh]">1.) State-of-the-art Dialect-MT Performance</li>
					<!-- <br>
					<ul class="b text-[2.1vh]"> 
						<li>What is the performance of the current state-of-the-art models in translating dialects?</li>
					</ul> -->
					<br>
					<li class="text-[5.1vh]">2.) Linguistic Information for Synthetic Sentences</li>
					<!-- <br>
					<ul class="b text-[2.1vh]"> 
						<li>Can we incorporate linguistic information in MT to synthetically generate sentences in language variants so that dialects of various <br> (and especially low-resource) languages can be processed more efficiently?</li>
					</ul> -->
					<br>
					<li class="text-[5.1vh]">3.) Requirements of Different Languages</li>
					<!-- <br>
					<ul class="b text-[2.1vh]"> 
						<li>What are requirements for deriving tools and processes that can be applied to vastly different languages from various language families?</li>
					</ul> -->
					<br>
					<!-- <li class="text-[5.1vh]">(4.) Role of Approaches</li>
					<br>
					<ul class="b text-[2.1vh]"> 
						<li>When using synthetic data, what roles do state-of-the-art approaches in fine-tuning, transfer learning and adapters play in improving the performance of MT systems to process (particularly low-resource) language variations effectively?</li>
					</ul> -->
				</ul>
			</div>
		</mybody>
	</Layout></Slide>
	
	<div class="text-[1.1vh]"></div>

	<Slide><Layout>
		<titlebar > Exploring Dialect Machine Translation </titlebar>
		<mybody>
			<div class="flex items-center justify-center">
				<figure class="mx-auto my-auto" >
					<img src="exploratory-2023_11_28-benglai.png" alt="exploringDialectMT">
					<figcaption class="text-[2.0vh]">
						GT: Google Translate (https://translate.google.com/) via the translate-shell (https://github.com/soimort/translate-shell),
						<br> NLLB: No Language Left Behind (Team et al., 2022), data primarily from CODET (Alam, Ahmadi, and Anastasopoulos, 2023)
					</figcaption>
					<!-- <figcaption class="text-[1.8vh]">
						These exploratory experiments utilized the translation systems Google Translate (https://translate.google.com/) 
						<br> via the translate-shell (https://github.com/soimort/translate-shell) 
						<br> and NLLB (Team et al., 2022), various data sets (primarily CODET (Alam, Ahmadi, and Anastasopoulos, 2023)), 
						<br> and the implementation of BLEU from Fairseq (https://github.com/facebookresearch/fairseq).
					</figcaption> -->
				</figure>
			</div>
		</mybody>
	</Layout></Slide>

	<Slide><Layout>
		<titlebar > Exploring Dialect Machine Translation </titlebar>
		<mybody>
			<div class="grid mx-auto my-auto" style="grid-template-columns: auto auto auto;">
				<!-- <figure class="mx-auto my-auto h-[85%] w-[85%]" >
					<img src="exploratory-2023_11_28-benglai.png" alt="exploringDialectMT">
				</figure> -->

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
				<figcaption class="text-[2.4vh]">
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
				<video controls class="w-[100%] mx-auto my-auto p-2">
					<source src="/video/german_dialects.mp4" type="video/mp4" />
					<track kind="captions" label="English" srclang="eng" src="media-video-captions-eng.vtt"/>
					<track kind="captions" label="German" srclang="deu" src="media-video-captions-deu.vtt" default/>
				</video>
				<figcaption class="text-[3.2vh]"> 
					Peter Frankenfeld - Die Wetterkarte - Deutsche Dialekte 	
				<div class="text-[2.1vh]">
					<br> (Source: https://www.youtube.com/watch?v=btlGMBA2XO4)
				</div>
				</figcaption>
			</figure>
		</mybody>
	</Layout></Slide>
	
	<Slide><Layout>
		<titlebar > German as Dialect Continuum </titlebar>
		<mybody  class="mt-[-1%]">
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
		<mybody  class="mt-[-1%]">
			<div class="flex items-center justify-center h-[90%]">
				<figure class="mx-auto my-auto h-[100%] w-[100%]" >
					<img src="images/Lameli_2008_German_Dialect_Continuum_Table.png" alt="datacleaning" style="max-height:100%; max-width:100%;">
				<figcaption class="text-[2.4vh]">
					(Lameli, 2008) displays the phonetic changes across German-speaking regions.
					<div class="text-[1.1vh]">
						<br> (Source: https://aktuell.nationalatlas.de/wp-content/uploads/08_09_Dialektraeume.pdf)
					</div>
				</figcaption>
				</figure>
			</div>
		</mybody>
	</Layout></Slide>

	<Slide><Layout>
		<titlebar > German </titlebar>
		<mybody class="mt-[-1%]">
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
		<titlebar > (German) Language Varieties </titlebar>
		<mybody class="mt-[-1%]">
			<div class="flex items-center justify-center h-[90%]">
				<figure class="mx-auto my-auto h-[100%] w-[100%]" >
					<img src="images/map-dialect-example-berliner-reddit.jpg" alt="datacleaning" style="max-height:100%; max-width:100%;">
				<figcaption class="text-[1.8vh]">
					(BaFi01, 2023) Es heist Berliner !
					<div class="text-[1.1vh]">
						<br> (Source: https://www.reddit.com/r/deutschememes/comments/15tumg7/es_heist_berliner/)
					</div>
				</figcaption>
				</figure>
			</div>

			<div class="flex items-center justify-center h-[90%]">
				<figure class="mx-auto my-auto h-[100%] w-[100%]" >
					<img src="images/map-dialect-example-berliner-bzberlin.jpg" alt="datacleaning" style="max-height:100%; max-width:100%;">
				<figcaption class="text-[1.8vh]">
					(BZ Die Stimme Berlins, 2014) Berliner, Pfannkuchen – ja, was denn nun?
					<div class="text-[1.1vh]">
						<br> (Source: https://www.bz-berlin.de/archiv-artikel/berliner-pfannkuchen-ja-was-denn-nun)
					</div>
				</figcaption>
				</figure>
			</div>

			<div class="flex items-center justify-center h-[90%]">
				<figure class="mx-auto my-auto h-[100%] w-[100%]" >
					<img src="images/map-dialect-example-berliner-atlasalltagssprache.jpg" alt="datacleaning" style="max-height:100%; max-width:100%;">
				<figcaption class="text-[1.8vh]">
					(Atlas zur deutschen Alltagssprache, 2011) Berliner/Krapfen
					<div class="text-[1.1vh]">
						<br> (Source: https://www.atlas-alltagssprache.de/runde-4/f03/)
					</div>
				</figcaption>
				</figure>
			</div>
		</mybody>
	</Layout></Slide>



	<script>newChapter("Methods & Experiments");</script>
	<Slide><Layout>
		<titlebar > Bilingual Lexicon Induction </titlebar>
		<mybody>
			<div class="flex items-center justify-center">
				<figure class="mx-auto my-auto h-[100%] w-[100%]" >
					<img src="ChameleonMT-BLI-BLI.png" alt="bli" style="max-height:100%; max-width:100%;">
				<figcaption class="text-[2.4vh]">
					Inspiration for this figure: (Irvine and Callison-Burch, 2017) A Comprehensive Analysis of Bilingual Lexicon Induction
					<br> (Wang et al., 2021) Porject Report - Training Domain Specific Multilingually Aligned Word Embeddings
				</figcaption>
				</figure>
			</div>
		</mybody>
	</Layout></Slide>

	<Slide><Layout>
		<titlebar > Aligning Vector Spaces via MUSE </titlebar>
		<mybody>
			<div class="flex items-center justify-center">
				<figure class="mx-auto my-auto h-[100%] w-[100%]" >
					<img src="images/MA-Thesis-BLI-MUSE-Fig1.png" alt="MUSE" style="max-height:100%; max-width:100%;">
				<figcaption class="text-[2.4vh]">
					(Conneau et al., 2018) introduced MUSE:
					<br> Figure 1: Toy illustration of the method. (A) There are two distributions of word embeddings, English words
					in red denoted by X and Italian words in blue denoted by Y , which we want to align/translate. Each dot
					represents a word in that space. The size of the dot is proportional to the frequency of the words in the training
					corpus of that language. (B) Using adversarial learning, we learn a rotation matrix W which roughly aligns the
					two distributions. The green stars are randomly selected words that are fed to the discriminator to determine
					whether the two word embeddings come from the same distribution. (C) The mapping W is further refined via
					Procrustes. This method uses frequent words aligned by the previous step as anchor points, and minimizes an
					energy function that corresponds to a spring system between anchor points. The refined mapping is then used
					to map all words in the dictionary. (D) Finally, we translate by using the mapping W and a distance metric,
					dubbed CSLS, that expands the space where there is high density of points (like the area around the word
					“cat”), so that “hubs” (like the word “cat”) become less close to other word vectors than they would otherwise
					(compare to the same region in panel (A)).
				</figcaption>
				</figure>
			</div>
		</mybody>
	</Layout></Slide>

	<Slide><Layout>
		<titlebar > MUSE is Dead - Long live DialectBLI </titlebar>
		<mybody>
			<div class="flex items-center justify-center">
				<figure class="mx-auto my-auto h-[100%] w-[100%]" >
					<img src="MUSE-github-issue-sina.png" alt="MUSE" style="max-height:100%; max-width:100%;">
				<figcaption class="text-[2.4vh]">
					Found my error message in an github-issue, which never got solved.
					<br> MUSE was archived on Oct 31, 2023.
				</figcaption>
				</figure>
			</div>
			<br>
			<div class="flex items-center justify-center">
				<figure class="mx-auto my-auto h-[100%] w-[100%]" >
					<img src="images/MA-Thesis-BLI-DialectBLI-Table1.png" alt="MUSE" style="max-height:100%; max-width:100%;">
				<figcaption class="text-[2.4vh]">
					(Artemova & Plank, 2023) Released BLI results for Bavarian and Alemannic.
				</figcaption>
				</figure>
			</div>
		</mybody>
	</Layout></Slide>

	<!-- <Slide><Layout>
		<titlebar > Linguistic Features </titlebar>
		<mybody>
			<div class="flex items-center justify-center">
				<figure class="mx-auto my-auto h-[100%] w-[100%]" >
					<img src="ChameleonMT-SYNTH-SYNTH.png" alt="datacleaning" style="max-height:100%; max-width:100%;">
				<figcaption class="text-[1.8vh]">
					The path to creating and using synthetic data.
				</figcaption>
				</figure>
			</div>
		</mybody>
	</Layout></Slide> -->

	<Slide><Layout>
        <titlebar> The Idea </titlebar>
        <mybody>
            <div class="flex items-center justify-center">
                <figure class="mx-auto my-auto h-[100%] w-[100%]" >
                        <img src="ChameleonMT-Concept-InitialConcept.png" alt="pathToSyntheticData" style="max-height:100%; max-width:100%;">
                    <figcaption class="text-[4.3vh]">
                        Initial concept of what to do.
                    </figcaption>
                </figure>
            </div>
        </mybody>
    </Layout></Slide>

	<Slide><Layout>
        <titlebar> The Plan </titlebar>
        <mybody>
            <div class="flex h-full items-center justify-center gap-[100px]">
                <figure class="h-[75vh] w-[80vw] float-left mx-auto my-auto" style="overflow:auto">
                        <img src="ChameleonMT-SYNTH-SYNTH.png" alt="pathToSyntheticData" style="display:inline">
                    <figcaption class="text-[4.3vh]">
                        The path to creating and using synthetic data.
                    </figcaption>
                </figure>
            </div>
        </mybody>
    </Layout></Slide>

	<Slide><Layout>
        <titlebar> The Reality </titlebar>
        <mybody>
            <div class="flex h-full items-center justify-center gap-[100px]">
                <figure class="h-[85vh] w-[100vw] float-left mx-auto my-auto" style="overflow:auto">
                        <img src="MA-Thesis-Overview.png" alt="pathToSyntheticData" style="display:inline">
                    <figcaption class="text-[4.3vh]">
                        The descent into madness.
                    </figcaption>
                </figure>
            </div>
        </mybody>
    </Layout></Slide>

	<Slide><Layout>
		<titlebar > Linguistic Features </titlebar>
		<mybody>
			<div class="flex items-center justify-center">
				<figure class="mx-auto my-auto h-[100%] w-[100%]" >
					<img src="MA-Thesis-Feature-Extraction-Example.png" alt="featureExtraction" style="max-height:100%; max-width:100%;">
				<figcaption class="text-[1.8vh]">
					Derived via string matching on aligned words.
				</figcaption>
				</figure>
			</div>

			<div class="flex items-center justify-center">
				<figure class="mx-auto my-auto h-[100%] w-[100%]" >
					<img src="MA-Thesis-Feature-Extraction-Example_0.png" alt="featureExtraction" style="max-height:100%; max-width:100%;">
				<figcaption class="text-[1.8vh]">
					From linguistic features to replacement rule (candidates).
				</figcaption>
				</figure>
			</div>

			<div class="flex items-center justify-center">
				<figure class="mx-auto my-auto h-[100%] w-[100%]" >
					<img src="MA-Thesis-Feature-Extraction-Example_1.png" alt="featureExtraction" style="max-height:100%; max-width:100%;">
				<figcaption class="text-[1.8vh]">
					Considering the context of (un-)matched sub-word units.
				</figcaption>
				</figure>
			</div>
		</mybody>
	</Layout></Slide>

	<!--
	Bavarian → German "reason" (u_number >= 5 && u_length =< 5) and context_length = 1 
		Prefixes: 47 lines 
		Suffixes: 292 lines
		Infixes: 138 lines

	Bavarian → German "relaxed" (u_number >= 1 && u_length =< 6) and context_length = 1 
		Prefixes: 507 lines 
		Suffixes: 1093 lines
		Infixes: 768 lines
	-->

	<!-- 
	TODO: (14/29) Synthetic Data
	Examples from my work
	-->
	<Slide><Layout>
		<titlebar > Synthetic Data </titlebar>
		<mybody>
			<div class="flex items-center justify-center">
				<figure class="mx-auto my-auto h-[60%] w-[60%]" >
					<img src="construction-itsupport.png" alt="relatedworkview" style="max-height:100%; max-width:100%;">
				<figcaption class="text-[1.8vh]">
					Results
				</figcaption>
				</figure>
			</div>
		</mybody>
	</Layout></Slide>
	
	<!-- 
	TODO: (15/29) Evaluation Metrics
	Issues with BLEU
	-->
	<Slide><Layout>
		<titlebar > Evaluation Metrics </titlebar>
		<mybody>
			<div class="flex items-center justify-center">
				<figure class="mx-auto my-auto h-[60%] w-[60%]" >
					<img src="construction-itsupport.png" alt="relatedworkview" style="max-height:100%; max-width:100%;">
				<figcaption class="text-[1.8vh]">
					Results
				</figcaption>
				</figure>
			</div>
		</mybody>
	</Layout></Slide>


	<!-- 
	TODO: (16/29) Data Cleaning 
	Highlight ~2 (important) examples to talk about.
	-->
	<Slide><Layout>
		<titlebar > Data Cleaning </titlebar>
		<mybody>
			<div class="flex items-center justify-center h-[100%]">
				<figure class="mx-auto my-auto w-[100%]" >
					<!-- <a href="URL_HERE"> -->
						<img src="ChameleonMT-DATA-DialectBLI02.png" alt="datacleaning" class="w-[85vw]">
					<!-- </a> -->
					<figcaption class="text-[2.3vh]">
						Examples of "aligned" Bavarian and Standard German sentences that have been excluded from the dataset 
						<br> (smaller font indicates content missing in the other variant's sentence)

					</figcaption>
				</figure>
			</div>
		</mybody>
	</Layout></Slide>

	<Slide><Layout>
		<titlebar > Data Cleaning </titlebar>
		<mybody>
			<div class="flex items-center justify-center h-[100%]">
				More than 20% non-German characters.

			</div>
		</mybody>
	</Layout></Slide>


	<!-- 
	TODO: (17/29) What I got out of it [Results]
	Tables from Overleaf and some sentences?
	-->
	<script>newChapter("Results");</script>
	<Slide><Layout>
		<titlebar > What I got out of it</titlebar>
		<mybody>
			<div class="flex items-center justify-center">
				<figure class="mx-auto my-auto h-[60%] w-[60%]" >
					<img src="construction-itsupport.png" alt="relatedworkview" style="max-height:100%; max-width:100%;">
				<figcaption class="text-[1.8vh]">
					Results
				</figcaption>
				</figure>
			</div>
		</mybody>
	</Layout></Slide>


	<!-- 
	TODO: ? New Slide ? Me and ma sea of Papers
	When I say "There is no data", I mean "I did not find any data", which does *NOT* equate to a two-minute-google-search . . .
	→ This is not bragging... It would probably have been reasonable to read less than I did by now and more than one person in this room tried to stop me XD
	-->


	
	<!-- <script>newChapter("Main Challenge");</script> -->
	<script>newChapter("Related Work");</script>
	<Slide><Layout>
		<titlebar > Related Work </titlebar>
		<mybody class="mt-[-2%]">
			<figure class="mx-auto my-auto h-[80%] w-[40%]" >
				<img src="construction-itsupport.png" alt="relatedworkview" style="max-height:100%; max-width:100%;">
			<figcaption class="text-[2.8vh]">
				Impressions of related work.
			</figcaption>
			</figure>

			<div class="h-[90%] w-[40%] mx-auto my-auto">
				<iframe src="pdf/2024_MA_Thesis_Christian_Schuler_RelatedWork.pdf#page=1&zoom=80" frameBorder="0" scrolling="auto" height="100%" width="100%" title="ESSV Publication"></iframe>
			</div>
		</mybody>
	</Layout></Slide>

	<Slide><Layout>
		<titlebar > Inspiration - Cross-Dialectal English NLP</titlebar>
		<mybody>
			<div class="flex items-center justify-center">
				<ul class="a" >
					<li>VALUE (Ziems et al., 2022) & Multi-VALUE (Ziems et al., 2023)</li>
					<br>
					<ul class="b"> 
						<li>50 English dialects and 29 - 136 linguistic features each </li> <!-- Aboriginal English, Australian English, Chicano English, Indian English, Sri Lankan English, Welsh English, ... -->
						<li>Examples: 
							<ul class="c">
								<li>Where are your books? - Where are y’all’s books? (your_yalls)</li> <!-- your_yalls -->
								<li>That isn’t fair. - That ain’t fair. (aint_be)</li> <!-- aint_be -->
								<li>She is at home. - She at home. (drop_copula_be_locative)</li> <!-- drop_copula_be_locative -->
								<li>When is she coming? - When she coming? (drop_aux_wh)</li> <!-- drop_aux_wh -->
							</ul> 
						
					</ul>
					<br>
				</ul>
			</div>
		</mybody>
	</Layout></Slide>
	

	<!-- 
	TODO: (18/29) Origin of the Noise - Bavarian Dialect Families
	Highlight the "Mittelbairisch" for next slide transition
	-->
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


	<!-- 
	TODO: (19/29) Origin of the Noise - Bavarian Varieties
	Highlight a few words to talk about and show differences.
	Rework caption and maybe move it next to table? Highlight the english part?
	-->
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
		<mybody class="mt-[-2%]">
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
	

	<!-- 
	TODO: (21/29) Origin of the Noise - Alpine Region
	Highlight or otherwise make crytal clear, that we have to cross (multiple) country borders now.
	-->
	<Slide><Layout>
		<titlebar > Origin of the Noise - Alpine Region</titlebar>
		<mybody class="mt-[-2%]">
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
						<img src="images/German-Varieties-20240405134346025.webp" alt="datacleaning" style="height: 100%;width: auto;">
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
	

	<!-- 
	TODO: + New Slide ? Mapping of Bavarian variants between works and datasets (From Obsidian) ?
	-->

	
	
	<script>newChapter("Next Steps");</script>

	<!-- 
	TODO: (23/29) Sorting Wikipedia Articles - Alemannic Example
	→ Title: Falling Down (the Rabbit Hole)
	-->
	<Slide><Layout>
		<titlebar > Sorting Wikipedia Articles - Alemannic Example </titlebar>
		<mybody class="mt-[-2%]">
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

	<!-- 
	TODO: (24/29) Sorting Wikipedia Articles - Alemannic Example
	Crop out "Alagnadeutsch" and "Issimedeutsch"
	→ Title: "12 Angry Subdialects"
	-->
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

	<!-- 
	TODO: (25/29) Sorting Wikipedia Articles - Alemannic Example
	→ Title: Good Word Hunting
	-->
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
	
	<!-- 
	TODO: + New Slide ? (Lambrecht et al., 2022): "Splitting into Alemannic variants shows great improvements"
	Also talk about how they just dropped the effing ball...
	→ Title: The Day The Wikidump Was Still Cleaned
	-->

	<!-- 
	TODO: (26/29) Sorting Wikipedia Articles - Current State
	→ Title: A Fistful Of Dialects
	-->
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

	<Slide><Layout>
		<titlebar class="text-[4.5vh]"> Beyond German - Northern Kurdish (Kurmanjî) and Central Kurdish (Soranî) </titlebar>
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

	
	<!-- 
	TODO: (27/29) NLLB-Tuning
	→ Title: Two Hundred And One Languages
	-->
	<Slide><Layout>
		<titlebar > NLLB-Tuning </titlebar>
		<mybody>
			<div class="flex items-center justify-center">
				Once the quality of data cleaning and perturbation has reached the next step. 
			</div>
		</mybody>
	</Layout></Slide>



<!-- 
TODO: + New Slide ? → Slide Title Easter Eggs
The Unusual Suspects → The Usual Suspects (1995)
12 Angry Subdialects → 12 Angry Men (1957)
Falling Down (the Rabbit Hole) → Falling Down (1993)
Two Hundred And One Languages → One Hundred And One Dalmatians (1961)
Good Word Hunting → Good Will Hunting (1997)
A Fistful Of Dialects → A Fistful Of Dollars (1964)
The Day The Wikidump Was Still Cleaned → The Day The Earth Stood Still (1951)

The Good, The Bad And The Others → The Good, The Bad And The Ugly (1967)
Low-Res is Beautiful → Life is Beautiful (1997)
 -->



	<script>newChapter("Appendix");</script>

	<Slide><Layout>
		<titlebar > References </titlebar>
		<mybody class="mt-[-2%]">
			<div class="h-[90%] w-[90%] mx-auto my-auto">
				<iframe src="pdf/2024_MA_Thesis_Christian_Schuler_References.pdf#page=1&zoom=100" frameBorder="0" scrolling="auto" height="100%" width="100%" title="ESSV Publication"></iframe>
			</div>
		</mybody>
	</Layout></Slide>

	<Slide><Layout>
		<titlebar > Guiding Research Questions </titlebar>
		<mybody class="mt-[-2%]">
			<div class="flex items-center justify-center">
				<ul class="a" >
					<li class="text-[5.1vh]">1.) State-of-the-art Performance</li>
					<br>
					<ul class="b text-[2.1vh]"> 
						<li>What is the performance of the current state-of-the-art models in translating dialects?</li>
					</ul>
					<br>
					<li class="text-[5.1vh]">2.) Linguistic Information for Synthetic Sentences</li>
					<br>
					<ul class="b text-[2.1vh]"> 
						<li>Can we incorporate linguistic information in MT to synthetically generate sentences in language variants so that dialects of various <br> (and especially low-resource) languages can be processed more efficiently?</li>
					</ul>
					<br>
					<li class="text-[5.1vh]">3.) Requirements of Different Languages</li>
					<br>
					<ul class="b text-[2.1vh]"> 
						<li>What are requirements for deriving tools and processes that can be applied to vastly different languages from various language families?</li>
					</ul>
					<br>
					<li class="text-[5.1vh]">4.) Role of Approaches</li>
					<br>
					<ul class="b text-[2.1vh]"> 
						<li>When using synthetic data, what roles do state-of-the-art approaches in fine-tuning, transfer learning and adapters play in improving the performance of MT systems to process (particularly low-resource) language variations effectively?</li>
					</ul>
				</ul>
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
		img{
			margin-left: auto;
			margin-right: auto;
			width: 100%;
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
