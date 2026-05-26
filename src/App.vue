<script setup>
import { computed, onBeforeUnmount, onMounted, ref } from "vue";
import {
  ArrowUpRight,
  BookOpenCheck,
  CalendarDays,
  Code2,
  Download,
  FlaskConical,
  GraduationCap,
  HeartPulse,
  Home,
  Mail,
  MapPin,
  Microscope,
  Newspaper,
  UsersRound,
} from "@lucide/vue";

import portraitUrl from "../pic/1.png";
import masscubeUrl from "../pic/masscube.png";
import bagoUrl from "../pic/bago.svg";
import maffinUrl from "../pic/MAFFIN.svg";
import foldChangeUrl from "../pic/fc.svg";
import cvUrl from "../docs/Huaxu_Yu_CV.pdf";

const navItems = [
  { id: "home", label: "Home", icon: Home },
  { id: "research", label: "Research", icon: Microscope },
  { id: "people", label: "People", icon: UsersRound },
  { id: "publications", label: "Publications", icon: BookOpenCheck },
  { id: "news", label: "News", icon: Newspaper },
  { id: "contact", label: "Contact", icon: Mail },
];

const validTabs = new Set(navItems.map((item) => item.id));

const normalizeHash = () => {
  const id = window.location.hash.replace("#", "");
  return validTabs.has(id) ? id : "home";
};

const activeTab = ref("home");

const handleHashChange = () => {
  activeTab.value = normalizeHash();
};

const selectTab = (id) => {
  activeTab.value = id;
  window.history.replaceState(null, "", `#${id}`);
  window.scrollTo({ top: 0, behavior: "smooth" });
};

onMounted(() => {
  activeTab.value = normalizeHash();
  window.addEventListener("hashchange", handleHashChange);
});

onBeforeUnmount(() => {
  window.removeEventListener("hashchange", handleHashChange);
});

const activeItem = computed(
  () => navItems.find((item) => item.id === activeTab.value) || navItems[0],
);

const labStats = [
  { value: "May 2026", label: "Yu Lab founded at ZJU" },
  { value: "28+", label: "publications in metabolomics and mass spectrometry" },
  { value: "80k+", label: "MassCube downloads" },
  { value: "4", label: "open-source tool lines" },
];

const researchThemes = [
  {
    title: "High-Quality MS Data",
    kicker: "Analytical chemistry",
    text: "We push the limits of MS data acquisition for broader metabolite detection and characterization.",
    tags: ["LC-MS", "quantitative metabolomics", "self-optimizing MS"],
  },
  {
    title: "Computational Metabolomics",
    kicker: "Algorithms & software",
    text: "We develop next-generation algorithms for metabolomics and ensure robust software performance through careful benchmarking.",
    tags: ["MassCube", "bioinformatics", "artificial intelligence"],
  },
  {
    title: "Pancreatic Cancer",
    kicker: "Oncology",
    text: "We aim to understand pancreatic cancer biology through global analysis of the tumor metabolic microenvironment.",
    tags: [
      "tumor microenvironment",
      "cancer metabolism",
      "spatial metabolomics",
    ],
  },
  {
    title: "Large Cohort Studies",
    kicker: "Large-scale metabolomics",
    text: "We perform large-scale metabolomics studies across clinical and population cohorts to uncover disease mechanisms and exposure signatures.",
    tags: ["clinical cohorts", "epidemiology", "precision medicine"],
  },
];

const softwareProjects = [
  {
    name: "MassCube",
    summary:
      "A Python framework for end-to-end metabolomics data processing from raw files to phenotype classifiers.",
    image: masscubeUrl,
    alt: "MassCube workflow figure",
    link: "https://huaxuyu.github.io/masscubedocs/",
    accent: "teal",
  },
  {
    name: "BAGO",
    summary:
      "Bayesian optimization of LC separation gradients for stronger untargeted metabolomics performance.",
    image: bagoUrl,
    alt: "BAGO project figure",
    link: "https://www.researchsquare.com/article/rs-3338667/v1",
    accent: "gold",
  },
  {
    name: "MAFFIN",
    summary:
      "Metabolomics sample normalization using high-quality metabolic features and corrected signal intensities.",
    image: maffinUrl,
    alt: "MAFFIN normalization figure",
    link: "https://doi.org/10.1093/bioinformatics/btac355",
    accent: "rose",
  },
  {
    name: "Fold-change bias correction",
    summary:
      "Methods to understand and correct quantitative bias caused by nonlinear electrospray ionization responses.",
    image: foldChangeUrl,
    alt: "Fold-change bias correction figure",
    link: "https://pubs.acs.org/doi/10.1021/acs.analchem.0c00246",
    accent: "green",
  },
];

const publications = [
  {
    title:
      "MassCube: a Python framework for end-to-end metabolomics data processing from raw files to phenotype classifiers",
    venue: "Nature Communications",
    authors: "Yu, H., Ding, J., Shen, T., Liu, M., Li, Y., Fiehn, O.",
    citation: "Nature Communications, 2025, 16(1), 5487.",
    year: "2025",
    links: [
      {
        label: "DOI",
        url: "https://doi.org/10.1038/s41467-025-60640-5",
      },
      {
        label: "Project website",
        url: "https://huaxuyu.github.io/masscubedocs",
      },
    ],
    note: "Software downloads: 84.50k",
    noteUrl:
      "https://pepy.tech/projects/masscube?timeRange=threeMonths&category=version&includeCIDownloads=true&granularity=daily&viewType=line&versions=Total",
  },
  {
    title:
      "Quantitative challenges and their bioinformatic solutions in mass spectrometry-based metabolomics",
    venue: "Trends in Analytical Chemistry",
    authors: "Yu, H., Low, B., Zhang, Z., Guo, J., Huan, T.",
    citation: "Trends in Analytical Chemistry, 2023, 161, 117009.",
    year: "2023",
    links: [
      {
        label: "DOI",
        url: "https://doi.org/10.1016/j.trac.2023.117009",
      },
    ],
    note: "Review article",
  },
  {
    title:
      "MAFFIN: metabolomics sample normalization using maximal density fold change with high-quality metabolic features and corrected signal intensities",
    venue: "Bioinformatics",
    authors: "Yu, H., Huan, T.",
    citation: "Bioinformatics, 2022, 38(13), 3429-3437.",
    year: "2022",
    links: [
      {
        label: "DOI",
        url: "https://doi.org/10.1093/bioinformatics/btac355",
      },
    ],
  },
  {
    title:
      "Adaptive Box-Cox transformation: a highly flexible feature-specific data transformation to improve metabolomics data normality for better statistical analysis",
    venue: "Analytical Chemistry",
    authors: "Yu, H., Sang, P., Huan, T.",
    citation: "Analytical Chemistry, 2022, 94(23), 8267-8276.",
    year: "2022",
    links: [
      {
        label: "DOI",
        url: "https://doi.org/10.1021/acs.analchem.2c00503",
      },
    ],
  },
  {
    title:
      "Comprehensive assessment of the diminished statistical power caused by nonlinear electrospray ionization responses in mass spectrometry-based metabolomics",
    venue: "Analytica Chimica Acta",
    authors: "Yu, H., Huan, T.",
    citation: "Analytica Chimica Acta, 2022, 1200, 339614.",
    year: "2022",
    links: [
      {
        label: "DOI",
        url: "https://doi.org/10.1016/j.aca.2022.339614",
      },
    ],
  },
  {
    title:
      "Patterned signal ratio biases in mass spectrometry-based quantitative metabolomics",
    venue: "Analytical Chemistry",
    authors: "Yu, H., Huan, T.",
    citation: "Analytical Chemistry, 2021, 93(4), 2254-2262.",
    year: "2021",
    links: [
      {
        label: "DOI",
        url: "https://doi.org/10.1021/acs.analchem.0c04113",
      },
    ],
  },
  {
    title:
      "Computational variation: An under-investigated quantitative variability caused by automated data processing in untargeted metabolomics",
    venue: "Analytical Chemistry",
    authors: "Yu, H., Chen, Y., Huan, T.",
    citation: "Analytical Chemistry, 2021, 93(25), 8719-8728.",
    year: "2021",
    links: [
      {
        label: "DOI",
        url: "https://doi.org/10.1021/acs.analchem.0c03381",
      },
    ],
  },
  {
    title:
      "Fold-change compression: An unexplored but correctable quantitative bias caused by nonlinear electrospray ionization responses in untargeted metabolomics",
    venue: "Analytical Chemistry",
    authors: "Yu, H., et al., Huan, T.",
    citation: "Analytical Chemistry, 2020, 92(10), 7011-7019.",
    year: "2020",
    links: [
      {
        label: "DOI",
        url: "https://doi.org/10.1021/acs.analchem.0c00246",
      },
    ],
  },
  {
    title:
      "Parallel metabolomics and lipidomics enables the comprehensive study of mouse brain regional metabolite and lipid patterns",
    venue: "Analytica Chimica Acta",
    authors: "Yu, H., Xing, S., Nierves, L., Lange, P. F., Huan, T.",
    citation: "Analytica Chimica Acta, 2020, 1136, 168-177.",
    year: "2020",
    links: [
      {
        label: "DOI",
        url: "https://doi.org/10.1016/j.aca.2020.09.051",
      },
    ],
  },
];

const training = [
  {
    place: "University of California, Davis",
    role: "Postdoctoral researcher",
    period: "2023.5 - 2026.3",
    supervisor: "Prof. Oliver Fiehn",
  },
  {
    place: "University of British Columbia",
    role: "Ph.D. in Chemistry",
    period: "2019.5 - 2023.4",
    supervisor: "Prof. Tao Huan",
  },
  {
    place: "Zhejiang University",
    role: "B.Sc. in Chemistry, Qiushi Honors Program",
    period: "2014.9 - 2018.6",
  },
];

const opportunities = [
  "Students excited by analytical chemistry, clinical data, and software-driven discovery",
  "Postdoctoral researchers with experience in MS, bioinformatics, statistics, or clinical metabolomics",
  "Clinician-scientists and computational collaborators interested in translational metabolomics",
];

const newsItems = [
  {
    date: "2025",
    title: "MassCube published in Nature Communications",
    category: "Publication",
    text: "The MassCube framework supports end-to-end metabolomics data processing and phenotype modeling.",
  },
];

const socialLinks = [
  {
    label: "Google Scholar",
    href: "https://scholar.google.ca/citations?user=tQAb4wkAAAAJ&hl=en",
    icon: BookOpenCheck,
  },
  { label: "GitHub", href: "https://github.com/huaxuyu", icon: Code2 },
  {
    label: "LinkedIn",
    href: "https://www.linkedin.com/in/huaxu-yu-b99829219/",
    icon: GraduationCap,
  },
  {
    label: "MassCube Docs",
    href: "https://huaxuyu.github.io/masscubedocs/",
    icon: FlaskConical,
  },
];
</script>

<template>
  <div class="site-shell">
    <header class="site-header">
      <a class="brand" href="#home" @click.prevent="selectTab('home')">
        <span class="brand-mark" aria-hidden="true">
          <HeartPulse :size="25" :stroke-width="2.4" />
        </span>
        <span class="brand-copy">
          <strong>Yu Lab</strong>
          <small>Clinical metabolomics and open software</small>
        </span>
      </a>

      <nav class="tab-nav" aria-label="Primary navigation">
        <button
          v-for="item in navItems"
          :key="item.id"
          class="tab-button"
          :class="{ active: activeTab === item.id }"
          type="button"
          :aria-current="activeTab === item.id ? 'page' : undefined"
          @click="selectTab(item.id)"
        >
          <component :is="item.icon" :size="18" stroke-width="2" />
          <span>{{ item.label }}</span>
        </button>
      </nav>
    </header>

    <main class="page-shell">
      <div class="mobile-section-label">
        <component :is="activeItem.icon" :size="18" />
        <span>{{ activeItem.label }}</span>
      </div>

      <section v-if="activeTab === 'home'" class="tab-panel home-panel">
        <div class="home-hero">
          <div class="intro-block">
            <h1 class="hero-title">
              Computational metabolomics for clinical discovery
            </h1>
            <p class="lead">
              The Yu Lab aims to advance large-scale metabolomics for
              understanding cancer and other human disease.
            </p>
            <div class="action-row hero-actions">
              <button
                class="primary-action"
                type="button"
                @click="selectTab('research')"
              >
                <Microscope :size="18" />
                Research
              </button>
              <button
                class="secondary-action"
                type="button"
                @click="selectTab('people')"
              >
                <UsersRound :size="18" />
                Join the lab
              </button>
            </div>
          </div>

          <aside class="pi-summary" aria-label="Principal investigator summary">
            <img :src="portraitUrl" alt="Huaxu Yu" />
            <div>
              <p class="eyebrow">Principal Investigator</p>
              <h2>Huaxu Yu</h2>
              <div class="affiliation-lines">
                <p>Clinical Distinguished Researcher</p>
                <p>
                  First Affiliated Hospital of Zhejiang University School of
                  Medicine
                </p>
                <p>Hangzhou, China</p>
              </div>
            </div>
          </aside>
        </div>

        <div class="stat-strip" aria-label="Lab highlights">
          <article v-for="stat in labStats" :key="stat.label" class="stat-card">
            <strong>{{ stat.value }}</strong>
            <span>{{ stat.label }}</span>
          </article>
        </div>

        <section class="content-section">
          <div class="section-heading">
            <p class="eyebrow">Research focus</p>
            <h2>From raw spectra to clinical insight</h2>
            <p>
              We pair careful analytical chemistry with computational systems
              that make metabolomics data reproducible, interpretable, and
              useful for translational biomedical research.
            </p>
          </div>

          <div class="feature-grid">
            <article
              v-for="theme in researchThemes"
              :key="theme.title"
              class="theme-card"
            >
              <span class="theme-kicker">{{ theme.kicker }}</span>
              <h3>{{ theme.title }}</h3>
              <p>{{ theme.text }}</p>
            </article>
          </div>
        </section>

        <section class="content-section split-section">
          <div class="section-heading compact">
            <p class="eyebrow">Updates</p>
            <h2>News</h2>
          </div>
          <div class="news-list">
            <article
              v-for="item in newsItems"
              :key="item.title"
              class="news-item"
            >
              <CalendarDays :size="20" />
              <div>
                <span>{{ item.date }}</span>
                <h3>{{ item.title }}</h3>
                <p>{{ item.text }}</p>
              </div>
            </article>
          </div>
        </section>
      </section>

      <section v-else-if="activeTab === 'research'" class="tab-panel">
        <div class="page-title">
          <p class="eyebrow">Research</p>
          <h1>Instrumentation, software, and clinical metabolomics.</h1>
          <p>
            The lab develops integrated experimental and computational methods
            for metabolomics, spanning data acquisition, data processing,
            AI-assisted analysis, and biological interpretation.
          </p>
        </div>

        <div class="research-grid">
          <article
            v-for="theme in researchThemes"
            :key="theme.title"
            class="research-card"
          >
            <span>{{ theme.kicker }}</span>
            <h2>{{ theme.title }}</h2>
            <p>{{ theme.text }}</p>
            <div class="tag-row">
              <span v-for="tag in theme.tags" :key="tag">{{ tag }}</span>
            </div>
          </article>
        </div>

        <section class="content-section">
          <div class="section-heading">
            <p class="eyebrow">Platforms</p>
            <h2>Selected methods and software</h2>
            <p>
              These projects anchor the lab's approach to reliable measurement,
              data processing, and quantitative correction in metabolomics.
            </p>
          </div>

          <div class="project-grid">
            <article
              v-for="project in softwareProjects"
              :key="project.name"
              class="project-card"
              :class="`accent-${project.accent}`"
            >
              <div class="project-image">
                <img :src="project.image" :alt="project.alt" />
              </div>
              <div class="project-copy">
                <h3>{{ project.name }}</h3>
                <p>{{ project.summary }}</p>
                <a :href="project.link" target="_blank" rel="noreferrer">
                  Learn more
                  <ArrowUpRight :size="16" />
                </a>
              </div>
            </article>
          </div>
        </section>
      </section>

      <section v-else-if="activeTab === 'people'" class="tab-panel">
        <div class="page-title">
          <p class="eyebrow">People</p>
          <h1>A new lab for careful measurement and useful computation.</h1>
          <p>
            The Yu Lab is forming a team of analytical chemists, computational
            scientists, clinical collaborators, and students who want to make
            metabolomics more reliable and more clinically informative.
          </p>
        </div>

        <div class="people-layout">
          <article class="person-card featured-person">
            <img :src="portraitUrl" alt="Huaxu Yu" />
            <div>
              <span class="theme-kicker">Founder and PI</span>
              <h2>Huaxu Yu</h2>
              <p>
                Huaxu is a chemist and software developer specializing in mass
                spectrometry-based metabolomics. His work integrates analytical
                chemistry, bioinformatics, and open-source software to generate
                reliable clinical metabolomics insight.
              </p>
              <div class="person-training">
                <h3>Scientific background</h3>
                <article v-for="item in training" :key="item.place">
                  <span>{{ item.period }}</span>
                  <div>
                    <strong>{{ item.place }}</strong>
                    <p>{{ item.role }}</p>
                    <small v-if="item.supervisor">
                      Research supervisor: {{ item.supervisor }}
                    </small>
                  </div>
                </article>
              </div>
              <div class="person-actions">
                <a :href="cvUrl" target="_blank" rel="noreferrer">
                  <Download :size="16" />
                  CV
                </a>
                <a
                  href="https://scholar.google.ca/citations?user=tQAb4wkAAAAJ&hl=en"
                  target="_blank"
                  rel="noreferrer"
                >
                  <BookOpenCheck :size="16" />
                  Scholar
                </a>
              </div>
            </div>
          </article>

          <section class="join-card">
            <span class="theme-kicker">Joining</span>
            <h2>We are building the team.</h2>
            <p>
              The lab welcomes inquiries from people interested in MS
              metabolomics, computational biology, bioinformatics, clinical
              translation, and open scientific software.
            </p>
            <ul>
              <li v-for="item in opportunities" :key="item">{{ item }}</li>
            </ul>
            <a class="inline-action" href="mailto:huaxuyu@zju.edu.cn">
              <Mail :size="16" />
              Contact Huaxu
            </a>
          </section>
        </div>
      </section>

      <section v-else-if="activeTab === 'publications'" class="tab-panel">
        <div class="page-title">
          <p class="eyebrow">Publications</p>
          <h1>Selected publications in metabolomics and mass spectrometry.</h1>
          <p>
            The nine publications below highlight work on computational
            metabolomics, quantitative bias, normalization, and clinical-scale
            data processing. For the full and current publication record, visit
            Google Scholar.
          </p>
          <div class="action-row">
            <a
              class="primary-link"
              href="https://scholar.google.ca/citations?user=tQAb4wkAAAAJ&hl=en"
              target="_blank"
              rel="noreferrer"
            >
              <BookOpenCheck :size="18" />
              Google Scholar
            </a>
            <a
              class="secondary-link"
              :href="cvUrl"
              target="_blank"
              rel="noreferrer"
            >
              <Download :size="18" />
              Download CV
            </a>
          </div>
        </div>

        <div class="publication-list">
          <article
            v-for="publication in publications"
            :key="publication.title"
            class="publication-card"
          >
            <div class="publication-meta">
              <span>{{ publication.year }}</span>
              <strong>{{ publication.venue }}</strong>
            </div>
            <div>
              <h2>{{ publication.title }}</h2>
              <p>{{ publication.authors }}</p>
              <p class="publication-citation">{{ publication.citation }}</p>
              <div class="publication-links">
                <a
                  v-for="link in publication.links"
                  :key="link.label"
                  :href="link.url"
                  target="_blank"
                  rel="noreferrer"
                >
                  {{ link.label }}
                  <ArrowUpRight :size="16" />
                </a>
              </div>
              <a
                v-if="publication.noteUrl"
                class="publication-note"
                :href="publication.noteUrl"
                target="_blank"
                rel="noreferrer"
              >
                {{ publication.note }}
                <ArrowUpRight :size="14" />
              </a>
              <p v-else-if="publication.note" class="publication-note">
                {{ publication.note }}
              </p>
            </div>
          </article>
        </div>
      </section>

      <section v-else-if="activeTab === 'news'" class="tab-panel">
        <div class="page-title">
          <p class="eyebrow">News</p>
          <h1>Updates from Yu Lab</h1>
        </div>

        <div class="news-timeline-page">
          <article
            v-for="item in newsItems"
            :key="item.title"
            class="news-timeline-item"
          >
            <div class="news-date">
              <span>{{ item.date }}</span>
            </div>
            <div class="news-body">
              <span>{{ item.category }}</span>
              <h2>{{ item.title }}</h2>
              <p>{{ item.text }}</p>
            </div>
          </article>
        </div>
      </section>

      <section v-else class="tab-panel">
        <div class="page-title">
          <p class="eyebrow">Contact</p>
          <h1>Collaborations, positions, and project conversations.</h1>
        </div>

        <div class="contact-grid">
          <article class="contact-card">
            <Mail :size="24" />
            <h2>Email</h2>
            <a href="mailto:huaxuyu@zju.edu.cn">huaxuyu@zju.edu.cn</a>
          </article>
          <article class="contact-card">
            <MapPin :size="24" />
            <h2>Location</h2>
            <p>
              The First Affiliated Hospital of Zhejiang University School of
              Medicine
            </p>
            <p>Hangzhou, Zhejiang, China</p>
          </article>
        </div>

        <section class="contact-links" aria-label="External links">
          <h2>Links</h2>
          <a
            v-for="link in socialLinks"
            :key="link.label"
            class="contact-link-row"
            :href="link.href"
            target="_blank"
            rel="noreferrer"
          >
            <span>
              <component :is="link.icon" :size="18" />
              {{ link.label }}
            </span>
            <ArrowUpRight :size="16" />
          </a>
        </section>
      </section>
    </main>

    <footer class="site-footer">
      <span>Yu Lab</span>
      <span
        >First Affiliated Hospital, Zhejiang University School of Medicine</span
      >
      <span>huaxuyulab.com</span>
    </footer>
  </div>
</template>
