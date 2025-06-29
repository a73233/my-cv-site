<script>
  import { scrollToFooter } from "../utils/scrollUtils";
  import Step from "./Step.svelte";
  import { base } from "$app/paths";
  import { onMount } from "svelte";

  const titles = [
    "Luís Neto - Software Developer",
    '$echo "I should really update my LinkedIn"',
    "Luís Neto - Computer Scientist",
    '$echo "I made this, using SvelteKit"',
    "Luís Neto - Software Engineer",
    '$cat ./cv.txt',
  ];
  let titleIndex = 0;
  let interval;

  onMount(() => {
    document.title = titles[titleIndex];
    interval = setInterval(() => {
      titleIndex = (titleIndex + 1) % titles.length;
      document.title = titles[titleIndex];
    }, 30000);
    return () => clearInterval(interval);
  });

  let steps = [
    {
      name: "Relational and Non-Relational Database Systems",
      icon: "devicon-mongodb-plain",
      description: "",
      bottom_description: "Project Rating \u2192 19/20",
    },
    {
      name: "Refractoring Aging Code Base - Modular Programming in Java",
      icon: "devicon-java-plain",
      description: "",
      bottom_description: "Project Rating \u2192 18/20",
    },
    {
      name: "Exploring the Evolution of Artificial Neural Networks through Genetic Algorithms",
      icon: "devicon-csharp-plain",
      description: "",
      bottom_description: "Project Rating \u2192 18/20",
    },
  ];

  let steps_personal_projects = [
    {
      name: "Converting Excel file to AutoHotKey Script",
      icon: "devicon-rust-plain",
      description: "",
      bottom_description: "",
    },
    {
      name: "Barcode Scanning Inventory Management Application",
      icon: "devicon-kotlin-plain",
      description: "",
      bottom_description: "",
    },
    {
      name: "Merging data from multiple Excel files into a single Excel file",
      icon: "devicon-csharp-line",
      description: "",
      bottom_description: "",
    },
  ];

  let benefits = [
    {
      metric: "10x",
      name: "Always striving to learn more",
      description:
        "As a dedicated programmer, I'm constantly pursuing knowledge and growth. Technology evolves rapidly, so I embrace each day as a chance to expand my skills and staying up to date. I find inspiration in programming's endless possibilities, using every challenge and project to enhance my expertise. Whether it's learning a new language, mastering a framework, or solving complex problems, my curiosity drives me to understand, create, and adapt. This pursuit empowers me to be a more proficient and adaptable programmer, contributing to the software development landscape's ongoing evolution.",
    },
    {
      name: "Responsible and Dependable",
      description:
        "I take great pride in being responsible and dependable. I understand the impact of my work on people's lives and businesses. I prioritize delivering high-quality, efficiently, and well-documented code that meets project needs. I'm committed to meeting deadlines, clear communication, and addressing issues promptly. Clients and teammates can rely on my transparency and trustworthiness in every project. In the collaborative world of programming, I'm the one others can count on, making responsibility and dependability both a professional standard and a personal ethos.",
    },
    {
      name: "Flexible and Adaptable",
      description:
        "I embrace flexibility and adaptability as essential traits in my role as a programmer. Technology evolves rapidly, demanding agile problem-solving. I excel in various languages and eagerly learn new ones. I stay current with industry trends. I approach novel challenges with creativity. I adapt to diverse teams effectively bridging technical and non-technical gaps. In the dynamic world of programming, I'm well-prepared to tackle any obstacle and seize opportunities.",
    },
  ];

  let benefitRefs = [];
  let rotateX = 0;
  let rotateY = 0;
  let isHovering = false;
  let iconRefs = [];
  let iconsInView = false;
  let svelteIconRef;
  let tailwindIconRef;
  let iconsPop = false;

  function handleMouseMove(event) {
    const card = event.currentTarget;
    const rect = card.getBoundingClientRect();
    const x = event.clientX - rect.left;
    const y = event.clientY - rect.top;
    const centerX = rect.width / 2;
    const centerY = rect.height / 2;
    const rotateMax = 15; // degrees

    rotateY = ((x - centerX) / centerX) * rotateMax;
    rotateX = -((y - centerY) / centerY) * rotateMax;
    isHovering = true;
  }

  function handleMouseLeave() {
    rotateX = 0;
    rotateY = 0;
    isHovering = false;
  }

  onMount(() => {
    const observer = new IntersectionObserver(
      (entries) => {
        entries.forEach((entry) => {
          if (entry.isIntersecting) {
            entry.target.classList.add("scale-110");
          } else {
            entry.target.classList.remove("scale-110");
          }
        });
      },
      {
        threshold: 0.1
      }
    );

    benefitRefs.forEach((ref) => {
      observer.observe(ref);
    });

    // Icon observer for pop effect
    const iconObserver = new IntersectionObserver(
      (entries) => {
        entries.forEach((entry) => {
          if (entry.isIntersecting) {
            iconsPop = false; // reset in case user scrolls quickly
            setTimeout(() => {
              iconsPop = true;
              setTimeout(() => {
                iconsPop = false;
              }, 400); // match animation duration
            }, 500); // delay before starting the pop animation
          }
        });
      },
      { threshold: 0.8 }
    );
    if (svelteIconRef) iconObserver.observe(svelteIconRef);
    if (tailwindIconRef) iconObserver.observe(tailwindIconRef);

    return () => {
      benefitRefs.forEach((ref) => {
        observer.unobserve(ref);
      });
      if (svelteIconRef) iconObserver.unobserve(svelteIconRef);
      if (tailwindIconRef) iconObserver.unobserve(tailwindIconRef);
    };
  });
</script>

<main class="flex flex-col flex-1 p-4">
  <section
    id="introPage"
    class="grid grid-cols-1 lg:grid-cols-2 gap-10 py-8 sm:py-14"
  >
    <div
      class="flex flex-col lg:justify-center text-center lg:text-left gap-6 md:gap-8 lg:gap-10 z-10"
    >
      <h2 class="font-semibold text-4xl sm:text-5xl md:text-6xl">
        Hi! I'm <span class="poppins text-violet-400">Luís</span> Neto,
        <br />Software
        <span class="poppins text-violet-400">Developer</span>
      </h2>
      <div class="text-base sm:text-lg md:text-xl">
        <p>
          I'm a Licensed <span class="text-violet-400">Computer Scientist</span>
            with a Master's in
            <a 
              href="http://cp.eng.uminho.pt/prova.aspx?id=7464"
              aria-label="Link to my Master Thesis final evaluation"
              target="_blank" 
              class="text-violet-300 hover:text-violet-200 underline underline-offset-2 hover:underline-offset-4 transition-all"
            >Informatics Engineering</a> from the University
          of Minho.
        </p>
        <p class="py-5">
          I'm a pragmatist and a minimalist at heart always striving to find
          solutions in the most efficient and effective way possible.
        </p>
      </div>

      <button
        class="blueShadow mx-auto lg:mr-auto lg:ml-0 text-base sm:text-lg md:text-xl poppins relative overflow-hidden px-6 py-3 group rounded-full bg-white text-slate-950"
        on:click={scrollToFooter}
      >
        <div
          class="absolute top-0 right-full w-full h-full bg-violet-400 opacity-20 group-hover:translate-x-full z-0 duration-200"
        />
        <h4 class="relative z-9">Get in touch &rarr;</h4>
      </button>
    </div>
    <div 
      class="relative shadow-2xl grid place-items-center z-10"
      style="perspective: 1000px;"
      role="presentation"
      on:mousemove={handleMouseMove}
      on:mouseleave={handleMouseLeave}
    >
      <img
        src={"images/profile.avif"}
        alt="Luis Neto Profile"
        class="object-cover z-[2] max-h-[50vh] transition-transform duration-0"
        style="transform: 
          rotateX({rotateX}deg) 
          rotateY({rotateY}deg) 
          scale({isHovering ? 1.05 : 1}); 
          filter: drop-shadow({isHovering ? '0 0 20px rgba(139, 92, 246, 0.5)' : '0 0 0 transparent'})"
      />
    </div>
    <!-- <div  class="flex p-0.5 relative max-w-[700px] w-full mx-auto">
            <div
                class="absolute inset-0 overflow-hidden rounded-md flex items-center justify-center"
            >
                <div
                    class="bg-gradient-to-r absolute inset-[-20px]  from-violet-800 to-indigo-800 specialSpin"
                />
            </div>

            <img
                src={"images/zetane-engine.jpeg"}
                alt="Zetane Engine"
                class="w-full h-full object-cover z-[2]"
            />
        </div> -->
  </section>
  <section class="py-20 lg:py-32 flex flex-col gap-24 z-10" id="projects">
    <div class="flex flex-col gap-2 text-center">
      <h6 class="text-large sm:text-xl md:text-2xl">
        Professional, <span class="poppins text-violet-400">disciplined</span> and
        versatile.
      </h6>
      <h3 class="font-semibold text-3xl sm:text-4xl md:text-5xl">
        A glipse into my <span class="poppins text-violet-400">academic</span> journey.
      </h3>
    </div>
    <!-- <a
            href="https://www.youtube.com/watch?v=dQw4w9WgXcQ"
            target="_blank"
            class="mx-auto px-4 py-2 rounded-md border border-solid border-white flex items-center gap-2 -mb-4 sm:-mb-0 -mt-10 hover:border-violet-700 duration-200"
        >
            <i class="fa-regular fa-circle-play" />
            <p>Watch the video</p>
        </a> -->
    <div class="grid grid-cols-1 lg:grid-cols-3 gap-12 lg:gap-10">
      <Step step={steps[0]}>
        <ul class="py-10">
          <li>
            Structured, designed and created a complex relational database in <strong
              class="text-violet-400">MySQL</strong
            >;
          </li>
          <li>
            Created a Java algorithm capable of automatically exporting the data
            on a relational database in <strong class="text-violet-400"
              >MySQL</strong
            >
            and importing that information to a non-relational database in
            <strong class="text-violet-400">MongoDB</strong>.
          </li>
        </ul>
      </Step>

      <Step step={steps[1]}>
        <ul class="py-14">
          <li>
            Developed a new architecture capable of supporting the
            functionalities present in <a href="http://ivy.di.uminho.pt/" target="_blank" class="text-violet-300 hover:text-violet-200 underline underline-offset-2 hover:underline-offset-4 transition-all">Ivy Workbench</a
              >, a model based tool for the analysis of interactive systems
            designs, using the concept of modularity introduced in
            <strong class="text-violet-400">Java 9</strong>.
          </li>
        </ul>
      </Step>
      <Step step={steps[2]}>
        <ul>
          <li>
            Reverse engineered an application's memory space using dynamic and static analysis.
          </li>
          <li>Established a sensory layer from the data gathered from the reverse engineering process.</li>
          <li>
            Used the <strong class="text-violet-400">NEAT</strong> algorithm
            to generate, evaluate, evolve and complexify <strong
              class="text-violet-400">artificial neural networks</strong>.
          </li>
          <li>
            Developed a motor layer capable of emulating the output of the generated <strong class="text-violet-400"
              >neural networks</strong
            > back into the running process.
          </li>
          <li><strong class="text-violet-400">C#</strong> and embedded <strong class="text-violet-400">AutoIt</strong> were used for this project.</li>
          <li>
            Verifiable <a href="http://cp.eng.uminho.pt/prova.aspx?id=7464" aria-label="Link to my Master Thesis final evaluation" target="_blank" class="text-violet-300 hover:text-violet-200 underline underline-offset-2 hover:underline-offset-4 transition-all">here</a>. 
            Available on <a href="https://repositorium.sdum.uminho.pt/handle/1822/92593" target="_blank" class="text-violet-300 hover:text-violet-200 underline underline-offset-2 hover:underline-offset-4 transition-all">RepositoriUM</a>.
          </li>
        </ul>
      </Step>
    </div>

    <div class="flex flex-col gap-2 text-center">
      <h6 class="text-large sm:text-xl md:text-2xl">
        Reasonable, <span class="poppins text-violet-400">rational</span> and responsible.
      </h6>
      <h3 class="font-semibold text-3xl sm:text-4xl md:text-5xl">
        Some of my <span class="poppins text-violet-400">personal</span> projects.
      </h3>
    </div>

    <div class="grid grid-cols-1 lg:grid-cols-3 gap-12 lg:gap-10">
      <Step step={steps_personal_projects[0]}>
        <ul class="py-10">
          <li>
            Designed an application with an intuitive <strong
              class="text-violet-400">G.U.I.</strong
            >
            with custom parameters and settings;
          </li>
          <li>
            Capable of receiving data from an <strong class="text-violet-400"
              >Excel</strong
            >
            file and converting it into an
            <strong class="text-violet-400">AutoHotKey</strong> script that can
            be used to automate the process of inserting barcodes into a
            <strong class="text-violet-400">SAGE</strong> form for printing;
          </li>
          <li>
            Application made with <strong class="text-violet-400">Tauri</strong>
            framework.
            <strong class="text-violet-400">TypeScript, HTML and CSS</strong>
            was used for the frontend and
            <strong class="text-violet-400">Rust</strong> was used for the backend.
          </li>
        </ul>
      </Step>

      <Step step={steps_personal_projects[1]}>
        <ul class="py-14">
          <li>
            Created a fully fledged mobile application capable of importing and
            storing data from an <strong class="text-violet-400">Excel</strong>
            file with a specified format and use the device's camera to scan barcodes,
            compare them to the data stored in the local database to update and save
            the current amount in stock;
          </li>

          <li>
            Being able to export the updated data to an
            <strong class="text-violet-400">Excel</strong> file at any given time;
          </li>

          <li>
            Constructed using <strong class="text-violet-400">Kotlin</strong>
            and the
            <strong class="text-violet-400">Android Studio IDE</strong>.
          </li>
        </ul>
      </Step>
      <Step step={steps_personal_projects[2]}>
        <ul>
          <li>
            Architectured an application complete with an intuitive and easy to
            use <strong class="text-violet-400">G.U.I.</strong>
            with displayed custom parameters and settings, capable of receiving data
            from an <strong class="text-violet-400">Excel</strong> file and
            merging it to an existing
            <strong class="text-violet-400">Excel</strong>
            for the purposes of inventory safe keeping;
          </li>
          <li>
            The algorithm efficiently traverses the <strong
              class="text-violet-400">Excel</strong
            >
            file and compares the reference code of each item to the reference code
            of the items in the other
            <strong class="text-violet-400">Excel</strong>
            file, if a match is found the algorithm will then proceed to merge/increment
            the data from the secondary
            <strong class="text-violet-400">Excel</strong>
            file to the main <strong class="text-violet-400">Excel</strong> file;
          </li>

          <li>
            Acomplished in <strong class="text-violet-400">C#</strong>, using
            Windows Forms for the
            <strong class="text-violet-400">G.U.I.</strong>
          </li>
        </ul>
      </Step>
    </div>
  </section>

  <section
    id="about"
    class="py-20 pt-10 lg:pt-16 lg:py-32 flex flex-col gap-16 sm:gap-20 md:gap-24 relative"
  >
    <!-- <div class="z-[-1] bg-violet-950 w-screen left-1/2 -translate-x-1/2 top-0 h-full absolute"> </div> -->
    <div
      class="flex flex-col gap-2 text-center relative before:absolute before:top-0 before:left-0 before:w-2/3 before:h-1.5 before:bg-violet-700 after:absolute after:bottom-0 after:right-0 after:w-2/3 after:h-1.5 after:bg-violet-700 py-6"
    >
      <h6 class="text-large sm:text-xl md:text-2xl">Want to know more?</h6>
      <h3 class="font-semibold text-3xl sm:text-4xl md:text-5xl">
        A bit <span class="poppins text-violet-400">about</span> me.
      </h3>
    </div>
    <p class="mx-auto poppins font-semibold text-lg sm:text-xl md:text-2xl">
      I am . . .
    </p>
    <div class="flex flex-col gap-20 w-full mx-auto max-w-[820px]">
      {#each benefits as benefit, index}
        <!-- <div class="flex flex-col gap-2 mx-auto">
                    <div class="flex items-end gap-4">
                        <p
                            class="poppins text-6xl sm:text-7xl md:text-8xl text-slate-500 font-medium"
                        >
                            {benefit.metric}
                        </p>
                        <p
                            class="text-xl sm:text-2xl md:text-3xl capitalize pb-2"
                        >
                            {benefit.name}
                        </p>
                    </div>
                    <p class="text-center italic">- {benefit.description}</p>
                </div> -->
        <div class="flex gap-6 sm:gap-8">
          <p
            class="poppins text-4xl sm:text-5xl md:text-6xl text-slate-500 font-semibold"
          >
            0{index + 1}
          </p>
          <div class="flex flex-col gap-6 sm:gap-8">
            <h3 class="text-2xl sm:text-3xl md:text-5xl">
              {benefit.name}
            </h3>
            <p
            class="transition-transform duration-75"
            bind:this={benefitRefs[index]}
          >
            {benefit.description}
          </p>
          </div>
        </div>
      {/each}
    </div>
    <h5 class={" text-2xl sm:text-3xl font-semibold text-center poppins "}>
      The <span class="text-violet-400">Complete</span> Package
    </h5>
    <div
      class="flex flex-col overflow-x-auto gap-10 max-w-[900px] mx-auto w-full table-with-shadow text-lg"
    >
      <table class="bg-slate-900 rounded text-center">
        <thead class={"border-b border-solid border-slate-200"}>
          <tr class="">
            <th />
            <th class="whitespace-nowrap p-2 px-4">Candidate #1</th>
            <th class="whitespace-nowrap p-2 px-4">Candidate #2</th>
            <th class="whitespace-nowrap p-2 px-4">Candidate #3</th>
            <th class="bg-violet-900 text-white whitespace-nowrap p-4 px-8"
              >Me</th
            >
          </tr>
        </thead>
        <tbody>
          <tr class="border-b border-solid border-slate-200">
            <td
              class="border-r border-solid border-white pl-4 pr-8 py-4 font-semibold text-base"
              >Dedication</td
            >
            <td><i class="fa-solid fa-xmark text-slate-500" /></td>
            <td><i class="fa-solid fa-check text-green-500" /></td>
            <td><i class="fa-solid fa-xmark text-slate-500" /></td>
            <td><i class="fa-solid fa-check text-green-500" /></td>
          </tr>
          <tr class="border-b border-solid border-slate-200">
            <td
              class="border-r border-solid border-white pl-4 pr-8 py-4 font-semibold text-base"
              >Critical Thought</td
            >
            <td><i class="fa-solid fa-xmark text-slate-500" /></td>
            <td><i class="fa-solid fa-check text-green-500" /></td>
            <td><i class="fa-solid fa-check text-green-500" /></td>
            <td><i class="fa-solid fa-check text-green-500" /></td>
          </tr>
          <tr>
            <td
              class="border-r border-solid border-white pl-4 pr-8 py-4 font-semibold text-base"
              >Interpersonal Skills</td
            >
            <td><i class="fa-solid fa-check text-green-500" /></td>
            <td><i class="fa-solid fa-check text-green-500" /></td>
            <td><i class="fa-solid fa-xmark text-slate-500" /></td>
            <td><i class="fa-solid fa-check text-green-500" /></td>
          </tr>
          <tr class="border-t border-solid border-slate-200">
            <td
              class="border-r border-solid border-white pl-4 pr-8 py-4 font-semibold text-base"
              >Progamming Ability</td
            >
            <td><i class="fa-solid fa-check text-green-500" /></td>
            <td><i class="fa-solid fa-xmark text-slate-500" /></td>
            <td><i class="fa-solid fa-check text-green-500" /></td>
            <td><i class="fa-solid fa-check text-green-500" /></td>
          </tr>
        </tbody>
      </table>
    </div>
    <div class="mx-auto -mt-12 italic sm:hidden opacity-50">
      <p>Scroll to see more &rarr;</p>
    </div>
    <div class="mx-auto">
      <div class="flex items-center">
        <p class="md:text-2xl ml-2 px-2">Made with</p>
        <i
          class="devicon-svelte-plain"
          style="font-size: 3em;"
          bind:this={svelteIconRef}
          class:pop-animate={iconsPop}
        />
        <p class="md:text-2xl ml-2 px-2">and</p>
        <i
          class="devicon-tailwindcss-plain"
          style="font-size: 3em;"
          bind:this={tailwindIconRef}
          class:pop-animate={iconsPop}
        />
      </div>
    </div>
  </section>
</main>
