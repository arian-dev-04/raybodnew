<template>
  <div
    class="site-shell"
    :class="[
      `lang-${language}`,
      {
        'menu-open': mobileMenuOpen,
        scrolled,
        'page-ready': !isLoading,
      },
    ]"
    :dir="language === 'fa' ? 'rtl' : 'ltr'"
    :lang="language"
  >
    <!-- =====================================================
         PREMIUM LIQUID ORB LOADER
    ====================================================== -->
    <Transition name="loader">
      <div
        v-if="isLoading"
        class="page-loader"
        aria-label="Loading"
        role="status"
      >
        <div class="loader-atmosphere"></div>

        <div class="loader-glow loader-glow-1"></div>
        <div class="loader-glow loader-glow-2"></div>
        <div class="loader-glow loader-glow-3"></div>

        <div class="loader-particles" aria-hidden="true">
          <span v-for="n in 18" :key="n"></span>
        </div>

        <div class="loader-bubble-field" aria-hidden="true">
          <span
            v-for="bubble in loaderBubbles"
            :key="bubble.id"
            class="loader-bubble"
            :class="`loader-bubble-${bubble.id}`"
            :style="{
              '--x': `${bubble.x}%`,
              '--size': `${bubble.size}px`,
              '--delay': `${bubble.delay}s`,
              '--rise': `${bubble.rise}s`,
              '--hue': bubble.hue,
            }"
          >
            <i class="bubble-shine"></i>
            <i class="bubble-inner-glow"></i>
          </span>
        </div>

        <div class="loader-system" aria-hidden="true">
          <span class="loader-orbit loader-orbit-1"></span>
          <span class="loader-orbit loader-orbit-2"></span>
          <span class="loader-orbit loader-orbit-3"></span>

          <span class="loader-orbit-dot loader-orbit-dot-1"></span>
          <span class="loader-orbit-dot loader-orbit-dot-2"></span>
          <span class="loader-orbit-dot loader-orbit-dot-3"></span>

          <div class="loader-core">
            <span class="loader-core-glow"></span>
            <span class="loader-core-inner"></span>
            <span class="loader-core-highlight"></span>
          </div>
        </div>

        <div class="loader-label">
          <span>
            {{ language === "fa" ? "در حال بارگذاری" : "Loading" }}
          </span>

          <i></i>

          <strong>RP</strong>
        </div>
      </div>
    </Transition>

    <!-- =====================================================
         HEADER
    ====================================================== -->
    <header class="site-header">
      <div class="container header-inner">
        <a
          class="brand"
          href="#home"
          aria-label="Raybod Pouye home"
          @click="closeMobileMenu"
        >
          <span class="brand-mark" aria-hidden="true">
            <i v-for="n in 6" :key="n"></i>
          </span>

          <span class="brand-name">
            {{ language === "fa" ? "رایبد پویه" : "RAYBOD POUYE" }}
          </span>
        </a>

        <nav class="desktop-nav" aria-label="Primary navigation">
          <a
            v-for="item in navItems"
            :key="item.id"
            :href="`#${item.id}`"
            :class="{ active: activeSection === item.id }"
            @click="setActive(item.id)"
          >
            {{ item.label[language] }}
          </a>
        </nav>

        <div class="header-actions">
          <button
            class="language-switch"
            type="button"
            :aria-label="
              language === 'en' ? 'Switch to Persian' : 'Switch to English'
            "
            @click="toggleLanguage"
          >
            <span :class="{ active: language === 'en' }">EN</span>
            <span class="language-separator">/</span>
            <span :class="{ active: language === 'fa' }">FA</span>
          </button>

          <a class="talk-button desktop-only" href="#contact">
            <span>{{ t("header.talk") }}</span>
            <span class="talk-arrow">→</span>
          </a>

          <button
            class="menu-toggle"
            type="button"
            :aria-expanded="mobileMenuOpen"
            :aria-label="mobileMenuOpen ? 'Close menu' : 'Open menu'"
            @click="toggleMobileMenu"
          >
            <span></span>
            <span></span>
          </button>
        </div>
      </div>
    </header>

    <!-- =====================================================
         MOBILE NAV
    ====================================================== -->
    <Transition name="mobile-menu">
      <div v-if="mobileMenuOpen" class="mobile-menu">
        <div class="mobile-menu-backdrop" @click="closeMobileMenu"></div>

        <div class="mobile-menu-panel">
          <div class="mobile-menu-top">
            <span>{{ t("menu.label") }}</span>

            <button type="button" @click="closeMobileMenu">×</button>
          </div>

          <nav aria-label="Mobile navigation">
            <a
              v-for="item in navItems"
              :key="item.id"
              :href="`#${item.id}`"
              @click="
                setActive(item.id);
                closeMobileMenu();
              "
            >
              <span class="menu-number">{{ item.number }}</span>

              <span>{{ item.label[language] }}</span>

              <span class="menu-arrow">↗</span>
            </a>
          </nav>

          <div class="mobile-menu-bottom">
            <button
              type="button"
              class="mobile-language"
              @click="toggleLanguage"
            >
              {{ language === "en" ? "فارسی" : "English" }}
            </button>

            <a href="#contact" @click="closeMobileMenu">
              {{ t("header.talk") }}
              <span>→</span>
            </a>
          </div>
        </div>
      </div>
    </Transition>

    <main>
      <!-- ===================================================
           HERO
      ==================================================== -->
      <section id="home" class="hero section">
        <div class="hero-noise" aria-hidden="true"></div>

        <div class="hero-ambient hero-ambient-1" aria-hidden="true"></div>
        <div class="hero-ambient hero-ambient-2" aria-hidden="true"></div>

        <div class="container hero-container">
          <div class="scroll-rail" aria-hidden="true">
            <span class="scroll-rail-line">
              <span class="scroll-rail-dot"></span>
            </span>

            <span class="scroll-rail-text">
              {{ t("hero.scroll") }}
            </span>
          </div>

          <div class="hero-copy reveal is-visible">
            <div class="eyebrow">
              <span>{{ t("hero.eyebrow") }}</span>
              <i></i>
            </div>

            <h1 class="hero-title">
              <span>{{ t("hero.line1") }}</span>

              <span class="hero-title-accent">
                {{ t("hero.line2") }}
              </span>

              <span>{{ t("hero.line3") }}</span>

              <strong>{{ t("hero.line4") }}</strong>
            </h1>

            <p class="hero-description">
              {{ t("hero.description") }}
            </p>

            <div class="hero-actions">
              <a
                class="hero-round-button"
                href="#contact"
                :aria-label="t('hero.cta')"
              >
                <span>→</span>
              </a>

              <a class="hero-link" href="#contact">
                {{ t("hero.cta") }}
              </a>

              <span class="hero-divider"></span>

              <span class="hero-slide-number">01 / 06</span>
            </div>
          </div>

          <!-- =================================================
               HERO ART
          ================================================== -->
          <div class="hero-art" aria-hidden="true">
            <div class="art-shadow"></div>

            <div class="glass-petal petal-a"></div>
            <div class="glass-petal petal-b"></div>
            <div class="glass-petal petal-c"></div>
            <div class="glass-petal petal-d"></div>
            <div class="glass-petal petal-e"></div>

            <div class="glass-ribbon ribbon-a"></div>
            <div class="glass-ribbon ribbon-b"></div>

            <div class="main-glass-sphere">
              <span class="sphere-highlight"></span>
            </div>

            <div class="art-ring ring-1"></div>
            <div class="art-ring ring-2"></div>
            <div class="art-ring ring-3"></div>

            <span class="mini-sphere sphere-1"></span>
            <span class="mini-sphere sphere-2"></span>
            <span class="mini-sphere sphere-3"></span>
            <span class="mini-sphere sphere-4"></span>

            <div class="light-streak"></div>
          </div>

          <!-- =================================================
               HERO CARDS
          ================================================== -->
          <div class="hero-cards">
            <article class="hero-card product-card reveal reveal-delay-1">
              <div class="hero-card-title">
                <span class="status-dot"></span>

                <span>{{ t("hero.product.title") }}</span>
              </div>

              <p>
                {{ t("hero.product.description") }}
              </p>

              <div class="hero-card-footer">
                <span>→</span>
                <i></i>
              </div>
            </article>

            <aside
              class="hero-stats reveal reveal-delay-2"
              :aria-label="t('hero.stats.label')"
            >
              <div v-for="stat in stats" :key="stat.key" class="stat-item">
                <strong>{{ animatedStats[stat.key] }}{{ stat.suffix }}</strong>

                <span>{{ stat.label[language] }}</span>
              </div>
            </aside>
          </div>
        </div>
      </section>

      <!-- ===================================================
           ABOUT
      ==================================================== -->
      <section id="about" class="about section">
        <div class="container content-grid">
          <div class="section-caption reveal">
            <span>{{ t("about.caption") }}</span>
            <i></i>
          </div>

          <div class="about-content reveal reveal-delay-1">
            <h2 class="display-title">
              {{ t("about.title.line1") }}

              <em>
                {{ t("about.title.line2") }}
              </em>

              {{ t("about.title.line3") }}
            </h2>

            <p>
              {{ t("about.description") }}
            </p>

            <div class="about-stats">
              <div
                v-for="stat in aboutStats"
                :key="stat.key"
                class="about-stat"
              >
                <strong>{{ animatedStats[stat.key] }}+</strong>
                <span>{{ stat.label[language] }}</span>
              </div>
            </div>
          </div>
        </div>
      </section>

      <!-- ===================================================
           SERVICES
      ==================================================== -->
      <section id="services" class="services section">
        <div class="container">
          <div class="section-head reveal">
            <div class="section-caption">
              <span>{{ t("services.caption") }}</span>
              <i></i>
            </div>
          </div>

          <div class="services-grid">
            <article
              v-for="service in services"
              :key="service.number"
              class="service-item reveal"
            >
              <span class="service-number">
                {{ service.number }}
              </span>

              <div class="service-body">
                <h2>{{ service.title[language] }}</h2>

                <p>{{ service.description[language] }}</p>
              </div>
            </article>

            <a class="services-work-link reveal" href="#case-studies">
              <span class="services-orb">
                <span>✦</span>
              </span>

              <span>{{ t("services.work") }}</span>

              <strong>→</strong>
            </a>
          </div>
        </div>
      </section>

      <!-- ===================================================
           EXPERTISE
      ==================================================== -->
      <section id="expertise" class="expertise section">
        <div class="container expertise-grid">
          <div class="section-caption reveal">
            <span>{{ t("expertise.caption") }}</span>
            <i></i>
          </div>

          <div class="expertise-content reveal reveal-delay-1">
            <h2 class="display-title">
              {{ t("expertise.title.line1") }}

              <em>{{ t("expertise.title.line2") }}</em>
            </h2>

            <p>
              {{ t("expertise.description") }}
            </p>

            <div class="expertise-tags">
              <span
                v-for="tag in expertiseTags"
                :key="tag"
                :class="{ active: activeExpertiseTags.includes(tag) }"
              >
                {{ t(tag) }}
              </span>
            </div>
          </div>
        </div>
      </section>

      <!-- ===================================================
           TESTIMONIALS
      ==================================================== -->
      <section id="testimonials" class="testimonials section">
        <div class="container">
          <div class="section-head reveal">
            <div class="section-caption">
              <span>{{ t("testimonials.caption") }}</span>
              <i></i>
            </div>
          </div>

          <div class="testimonials-grid">
            <article
              v-for="item in testimonials"
              :key="item.name"
              class="testimonial-card reveal"
            >
              <div class="testimonial-card__box">
                <div class="testimonial-quote">“</div>

                <p>
                  {{ item.text[language] }}
                </p>

                <div class="testimonial-stars" aria-hidden="true">
                  <span v-for="star in 5" :key="star">
                    {{ star <= item.rating ? "★" : "☆" }}
                  </span>
                </div>
              </div>

              <div class="testimonial-client">
                <img
                  :src="item.image"
                  :alt="item.name"
                  loading="lazy"
                  draggable="false"
                />

                <div>
                  <strong>{{ item.name }}</strong>
                  <span>{{ item.role[language] }}</span>
                </div>
              </div>
            </article>
          </div>
        </div>
      </section>

      <!-- ===================================================
           CASE STUDIES
      ==================================================== -->
      <section id="case-studies" class="work section">
        <div class="container">
          <div class="work-top reveal">
            <div class="section-caption">
              <span>{{ t("case.caption") }}</span>
              <i></i>
            </div>

            <div>
              <h2 class="display-title">
                {{ t("case.title.line1") }}

                <em>
                  {{ t("case.title.line2") }}
                </em>
              </h2>
            </div>
          </div>

          <div class="work-grid">
            <article
              v-for="(project, index) in projects"
              :key="project.title.en"
              class="project reveal"
              :class="{ 'project-large': index === 0 }"
            >
              <div
                class="project-visual project-photo"
                :style="{
                  '--hue': project.hue,
                  '--project-image': `url('${project.image}')`,
                }"
              >
                <div class="project-overlay"></div>

                <div class="project-glow"></div>

                <div class="project-shape shape-one"></div>
                <div class="project-shape shape-two"></div>

                <div class="project-sphere"></div>

                <span class="project-orbit orbit-a"></span>
                <span class="project-orbit orbit-b"></span>
              </div>

              <div class="project-meta">
                <div>
                  <span>{{ project.category[language] }}</span>

                  <h3>{{ project.title[language] }}</h3>
                </div>

                <span class="project-arrow">↗</span>
              </div>
            </article>
          </div>
        </div>
      </section>

      <!-- ===================================================
           CTA
      ==================================================== -->
      <section class="cta section">
        <div class="container">
          <div class="cta-panel reveal">
            <div>
              <div class="section-caption">
                <span>{{ t("cta.caption") }}</span>
                <i></i>
              </div>

              <h2 class="display-title">
                {{ t("cta.title.line1") }}

                <em>{{ t("cta.title.line2") }}</em>
              </h2>

              <p>{{ t("cta.description") }}</p>
            </div>

            <a class="pill-link" href="#contact">
              <span>{{ t("cta.button") }}</span>
              <strong>↗</strong>
            </a>
          </div>
        </div>
      </section>

      <!-- ===================================================
           OFFICE / CONTACT
      ==================================================== -->
      <section id="contact" class="contact section">
        <div class="container contact-wrapper">
          <div class="office-content reveal">
            <div class="section-caption">
              <span>{{ t("office.caption") }}</span>
              <i></i>
            </div>

            <h2 class="display-title">
              {{ t("office.title.line1") }}

              <em>{{ t("office.title.line2") }}</em>
            </h2>

            <div class="contact-cards">
              <article class="contact-card">
                <span class="contact-card-label">
                  {{ t("office.headquarters") }}
                </span>

                <h3>{{ t("office.tehran") }}</h3>

                <p>
                  {{ t("office.address1") }}
                </p>

                <div class="contact-details">
                  <a :href="`tel:${contactData.phone1Raw}`">
                    {{ t("office.phone1") }}
                  </a>

                  <a :href="`mailto:${contactData.email}`">
                    {{ contactData.email }}
                  </a>
                </div>
              </article>

              <article class="contact-card">
                <span class="contact-card-label">
                  {{ t("office.branch") }}
                </span>

                <h3>{{ t("office.tehranBranch") }}</h3>

                <p>
                  {{ t("office.address2") }}
                </p>

                <div class="contact-details">
                  <a :href="`tel:${contactData.phone2Raw}`">
                    {{ t("office.phone2") }}
                  </a>

                  <a :href="`mailto:${contactData.email}`">
                    {{ contactData.email }}
                  </a>
                </div>
              </article>
            </div>
          </div>

          <div class="contact-visual reveal reveal-delay-1">
            <div class="contact-visual-glow"></div>

            <div class="contact-orbit orbit-contact-1"></div>
            <div class="contact-orbit orbit-contact-2"></div>

            <div class="contact-sphere"></div>

            <div class="contact-center">
              <span>RP</span>
            </div>

            <a class="contact-mail" :href="`mailto:${contactData.email}`">
              {{ contactData.email }}
            </a>
          </div>
        </div>
      </section>
    </main>

    <!-- =====================================================
         FOOTER
    ====================================================== -->
    <footer class="footer">
      <div class="container">
        <div class="footer-top">
          <div class="footer-brand-block">
            <a class="brand" href="#home">
              <span class="brand-mark" aria-hidden="true">
                <i v-for="n in 6" :key="n"></i>
              </span>

              <span class="brand-name">
                {{ language === "fa" ? "رایبد پویه" : "RAYBOD POUYE" }}
              </span>
            </a>

            <p>
              {{ t("footer.description") }}
            </p>

            <small>
              {{ t("footer.copyright") }}
            </small>
          </div>

          <div class="footer-columns">
            <div
              v-for="column in footerColumns"
              :key="column.key"
              class="footer-col"
              :class="{
                'is-open': openFooterSection === column.key,
              }"
            >
              <button
                type="button"
                class="footer-col__toggle"
                :aria-expanded="openFooterSection === column.key"
                @click="toggleFooterSection(column.key)"
              >
                <span>{{ t(column.title) }}</span>
                <span class="footer-col__arrow">⌄</span>
              </button>

              <div class="footer-col__links">
                <a
                  v-for="link in column.links"
                  :key="link.label"
                  :href="link.href"
                >
                  {{ t(link.label) }}
                </a>
              </div>
            </div>
          </div>
        </div>

        <div class="footer-bottom">
          <span>{{ t("footer.bottom") }}</span>

          <div class="footer-social">
            <div class="socials">
              <a href="#" aria-label="Facebook">f</a>
              <a href="#" aria-label="LinkedIn">in</a>
              <a href="#" aria-label="X">x</a>
              <a href="#" aria-label="Instagram">ig</a>
            </div>

            <select
              v-model="language"
              @change="changeLanguage(language)"
              aria-label="Language"
            >
              <option value="en">
                {{ t("footer.english") }}
              </option>

              <option value="fa">
                {{ t("footer.persian") }}
              </option>
            </select>
          </div>
        </div>
      </div>
    </footer>

    <!-- =====================================================
         BACK TO TOP
    ====================================================== -->
    <button
      class="to-top"
      type="button"
      aria-label="Back to top"
      :class="{ show: scrolled }"
      @click="scrollTop"
    >
      ↑
    </button>
  </div>
</template>

<script setup>
import { nextTick, onBeforeUnmount, onMounted, reactive, ref } from "vue";

/* =========================================================
   STATE
========================================================= */

const language = ref("en");
const isLoading = ref(true);
const mobileMenuOpen = ref(false);
const scrolled = ref(false);
const activeSection = ref("home");
const openFooterSection = ref(null);

let revealObserver = null;
let sectionObserver = null;
let statsAnimationFrame = null;
let loadingTimer = null;

/* =========================================================
   LOADER DATA
========================================================= */

const loaderBubbles = [
  {
    id: 1,
    x: 14,
    size: 96,
    delay: 0,
    rise: 1.35,
    hue: 235,
  },
  {
    id: 2,
    x: 28,
    size: 68,
    delay: 0.12,
    rise: 1.42,
    hue: 270,
  },
  {
    id: 3,
    x: 43,
    size: 115,
    delay: 0.18,
    rise: 1.55,
    hue: 205,
  },
  {
    id: 4,
    x: 58,
    size: 72,
    delay: 0.05,
    rise: 1.38,
    hue: 315,
  },
  {
    id: 5,
    x: 73,
    size: 52,
    delay: 0.22,
    rise: 1.48,
    hue: 185,
  },
  {
    id: 6,
    x: 87,
    size: 82,
    delay: 0.1,
    rise: 1.5,
    hue: 250,
  },
];

/* =========================================================
   TRANSLATIONS
========================================================= */

const translations = {
  en: {
    header: {
      talk: "Contact Us",
    },

    menu: {
      label: "MENU",
    },

    hero: {
      eyebrow: "SMART SOFTWARE ENGINEERING COMPANY",
      line1: "Smart",
      line2: "Solutions",
      line3: "for Your",
      line4: "Organization.",

      description:
        "Raybod Pouye is a leading company in consulting and development of intelligent software and innovative network solutions.",

      cta: "Let's Work Together",
      scroll: "Scroll",

      stats: {
        label: "Company statistics",
      },

      product: {
        title: "Intelligent Network Management",
        description:
          "Smart monitoring, management and automated troubleshooting.",
      },
    },

    about: {
      caption: "ABOUT US",

      title: {
        line1: "Intelligent software",
        line2: "solutions",
        line3: "for real organizational challenges.",
      },

      description:
        "Raybod Pouye is a leading company in consulting and development of intelligent software, providing innovative solutions in network communications. With advanced technologies and an expert team, we create secure, practical and scalable products for organizations.",
    },

    services: {
      caption: "OUR SERVICES",
      work: "View Our Projects",
    },

    expertise: {
      caption: "OUR EXPERTISE",

      title: {
        line1: "Technology",
        line2: "that works.",
      },

      description:
        "We combine modern technologies, artificial intelligence and deep technical expertise to build solutions tailored to organizational infrastructure.",

      tags: {
        Marketing: "Knowledge Management",
        SEO: "Artificial Intelligence",
        "Social Media": "Neural Networks",
        "Web Development": "Software Development",
        "UI Design": "System Design",
        "Mobile Apps": "Mobile Apps",
        Photography: "Technical Support",
        "Company Profile": "Network Security",
        "Visual Editing": "Databases",
      },
    },

    testimonials: {
      caption: "CLIENT TESTIMONIALS",
    },

    case: {
      caption: "SELECTED PROJECTS",

      title: {
        line1: "Projects",
        line2: "that matter.",
      },
    },

    cta: {
      caption: "LET'S COLLABORATE",

      title: {
        line1: "Have an organizational",
        line2: "challenge?",
      },

      description:
        "Contact us to start a collaboration and get expert consultation for your digital transformation journey.",

      button: "Contact Us",
    },

    office: {
      caption: "OUR OFFICE",

      title: {
        line1: "Let's build",
        line2: "something useful.",
      },

      headquarters: "HEADQUARTERS",
      branch: "BRANCH OFFICE",

      tehran: "Tehran Office",
      tehranBranch: "Tehran Branch",

      address1: "Tehran, University of Tehran, Qods St., Azin Alley, No. 4",

      address2: "Tehran, Valiasr St., No. 123, 3rd Floor",

      phone1: "+98-21-12345678",
      phone2: "+98-21-76543210",
    },

    footer: {
      description:
        "Raybod Pouye with 16 years of experience and more than 50 successful projects, a trusted partner for organizations on their digital transformation journey.",

      copyright: "© Raybod Pouye 2026",

      bottom: "Intelligent Software & Digital Solutions",

      COMPANY: "Company",
      SERVICES: "Services",
      RESOURCES: "Resources",

      english: "English - En",
      persian: "Persian - Fa",
    },

    service1: "Intelligent Network Management Software",
    service1_desc:
      "A comprehensive software for intelligent management and monitoring of organizational networks with automated troubleshooting capabilities.",

    service2: "Intelligent Search Engine & GPT Assistant",
    service2_desc:
      "An intelligent search engine with a GPT assistant that enables quick access to information across various organizational sources.",

    service3: "Raya Intelligent Knowledge Network",
    service3_desc:
      "Raya intelligent knowledge network, a platform for managing and exchanging knowledge within the organization.",

    service4: "Data Analytics Platform",
    service4_desc:
      "An advanced data analytics platform for organizational data with interactive and precise reporting.",

    service5: "Enterprise Integration Platform",
    service5_desc:
      "An integrated enterprise platform for connecting various organizational systems and facilitating data flow.",

    service6: "Network Security Solution",
    service6_desc:
      "A comprehensive network security solution with threat detection and rapid response to attacks.",

    Employee: "Years Experience",
    Projects: "Successful Projects",
    Clients: "Organizations",

    proj1: "Mobarakeh Steel Knowledge Management Project",
    proj2: "Sangan Steel Intelligent Network Project",
    proj3: "Public Libraries Management System",
    proj4: "Enterprise Search Engine",

    projectCategory1: "Knowledge Management",
    projectCategory2: "Network Management",
    projectCategory3: "Enterprise Software",
    projectCategory4: "Artificial Intelligence",

    test1:
      "The main difference of this project for us was starting knowledge management from real organizational problems, not from choosing tools. The consulting team designed and implemented solutions tailored to our needs with precise understanding of our processes and challenges.",

    test2:
      "One of the strengths of this collaboration was the fully practical approach of the consulting team. The project output was not just a set of documents; processes, roles, and mechanisms were established to enable the continuation and development of knowledge management in the organization.",

    test3:
      "Before using the system, identifying the source of network disruptions took a lot of time from our experts. The dashboards and centralized information of the software have made the diagnosis and resolution process much faster for our team.",

    test4:
      "For us, data security and control were very important. Using a native solution that can be deployed on organizational infrastructure allowed us to manage and monitor the network without relying on external services.",

    test5:
      "The high volume of organizational documents and information made it time-consuming for experts to find needed information. Raya's search engine and intelligent assistant enabled us to find information faster and more accurately from various organizational sources.",

    test6:
      "The main advantage of Raya's search engine for us is that search is not just based on word matching; the system can understand the meaning and relationship of the content and provide more relevant results to the user.",

    role1: "Head of Quality and Excellence Systems, Mobarakeh Steel Company",
    role2: "Industrial Engineering Manager, Sangan Steel Company",

    role3:
      "IT Director, General Directorate of Public Libraries of Kermanshah Province",

    role4: "IT Manager",
    role5: "Knowledge Manager",
    role6: "Senior Technology Expert",

    phone1: "+98-21-12345678",
    phone2: "+98-21-76543210",

    email: "info@raybidpouye.com",

    aboutLink: "About Us",
    serviceLink1: "Knowledge Management Consulting",
    serviceLink2: "Intelligent Software Development",
    serviceLink3: "Knowledge Systems Implementation",
    serviceLink4: "Support & Training",
    resourceLink1: "Documentation",
    resourceLink2: "Artificial Intelligence",
    resourceLink3: "Digital Transformation",
  },

  fa: {
    header: {
      talk: "تماس با ما",
    },

    menu: {
      label: "منو",
    },

    hero: {
      eyebrow: "شرکت مهندسی نرم‌افزار هوشمند",
      line1: "راهکارهای",
      line2: "هوشمند",
      line3: "برای",
      line4: "سازمان شما.",

      description:
        "رایبد پویه شرکتی پیشرو در زمینه مشاوره و تولید نرم‌افزارهای هوشمند و راهکارهای نوآورانه ارتباطات شبکه‌ای است.",

      cta: "شروع همکاری",
      scroll: "اسکرول",

      stats: {
        label: "آمار شرکت",
      },

      product: {
        title: "مدیریت هوشمند شبکه",
        description: "پایش، مدیریت و عیب‌یابی هوشمند و خودکار شبکه.",
      },
    },

    about: {
      caption: "درباره ما",

      title: {
        line1: "راهکارهای نرم‌افزاری",
        line2: "هوشمند",
        line3: "برای مسائل واقعی سازمان.",
      },

      description:
        "رایبد پویه شرکتی پیشرو در زمینه مشاوره و تولید نرم‌افزارهای هوشمند است که به توسعه و ارائه راهکارهای نوآورانه در زمینه انواع ارتباطات شبکه‌ای می‌پردازد. با بهره‌گیری از فناوری‌های روز دنیا و تیم متخصص، محصولاتی امن، کاربردی و متناسب با زیرساخت سازمان ارائه می‌کنیم.",
    },

    services: {
      caption: "خدمات ما",
      work: "مشاهده پروژه‌ها",
    },

    expertise: {
      caption: "تخصص ما",

      title: {
        line1: "فناوری",
        line2: "که کاربردی است.",
      },

      description:
        "ما با ترکیب فناوری‌های روز، هوش مصنوعی و تخصص فنی عمیق، راهکارهایی متناسب با زیرساخت و نیازهای سازمان طراحی و پیاده‌سازی می‌کنیم.",

      tags: {
        Marketing: "مدیریت دانش",
        SEO: "هوش مصنوعی",
        "Social Media": "شبکه‌های عصبی",
        "Web Development": "توسعه نرم‌افزار",
        "UI Design": "طراحی سیستم",
        "Mobile Apps": "اپلیکیشن موبایل",
        Photography: "پشتیبانی فنی",
        "Company Profile": "امنیت شبکه",
        "Visual Editing": "پایگاه داده",
      },
    },

    testimonials: {
      caption: "نظرات مشتریان",
    },

    case: {
      caption: "پروژه‌های منتخب",

      title: {
        line1: "پروژه‌هایی",
        line2: "با نتیجه واقعی.",
      },
    },

    cta: {
      caption: "شروع همکاری",

      title: {
        line1: "یک چالش سازمانی",
        line2: "دارید؟",
      },

      description:
        "برای شروع همکاری و دریافت مشاوره تخصصی در مسیر تحول دیجیتال سازمان با ما تماس بگیرید.",

      button: "تماس با ما",
    },

    office: {
      caption: "دفتر ما",

      title: {
        line1: "بیایید یک",
        line2: "راهکار کاربردی بسازیم.",
      },

      headquarters: "دفتر مرکزی",
      branch: "شعبه",

      tehran: "دفتر تهران",
      tehranBranch: "شعبه تهران",

      address1: "تهران، دانشگاه تهران، خیابان قدس، کوچه آذین، پلاک ۴",

      address2: "تهران، خیابان ولیعصر، پلاک ۱۲۳، طبقه ۳",

      phone1: "+۹۸-۲۱-۱۲۳۴۵۶۷۸",
      phone2: "+۹۸-۲۱-۷۶۵۴۳۲۱۰",
    },

    footer: {
      description:
        "رایبد پویه با ۱۶ سال تجربه و بیش از ۵۰ پروژه موفق، همراه مطمئن سازمان‌ها در مسیر تحول دیجیتال.",

      copyright: "© رایبد پویه ۱۴۰۵",

      bottom: "راهکارهای هوشمند نرم‌افزاری و سازمانی",

      COMPANY: "شرکت",
      SERVICES: "خدمات",
      RESOURCES: "منابع",

      english: "English - En",
      persian: "فارسی - Fa",
    },

    service1: "نرم‌افزار مدیریت هوشمند شبکه",
    service1_desc:
      "نرم‌افزاری جامع برای مدیریت و پایش هوشمند شبکه‌های سازمانی با قابلیت عیب‌یابی خودکار.",

    service2: "موتور جستجوی هوشمند و دستیار GPT",
    service2_desc:
      "موتور جستجوی هوشمند همراه با دستیار GPT برای دسترسی سریع به اطلاعات منابع مختلف سازمان.",

    service3: "شبکه دانش هوشمند رایا",
    service3_desc:
      "شبکه دانش هوشمند رایا، بستری برای مدیریت و تبادل دانش در سازمان.",

    service4: "سامانه تحلیل داده",
    service4_desc:
      "سامانه پیشرفته تحلیل داده‌های سازمانی با گزارش‌های دقیق و تعاملی.",

    service5: "پلتفرم یکپارچه سازمانی",
    service5_desc:
      "پلتفرمی برای اتصال سامانه‌های مختلف سازمان و تسهیل جریان داده.",

    service6: "راهکار امنیت شبکه",
    service6_desc:
      "راهکار جامع امنیت شبکه با قابلیت شناسایی تهدیدات و پاسخ سریع به حملات.",

    Employee: "سال تجربه",
    Projects: "پروژه موفق",
    Clients: "سازمان بزرگ",

    proj1: "پروژه مدیریت دانش فولاد مبارکه",
    proj2: "پروژه شبکه هوشمند فولاد سنگان",
    proj3: "سامانه مدیریت کتابخانه‌های عمومی",
    proj4: "موتور جستجوی سازمانی",

    projectCategory1: "مدیریت دانش",
    projectCategory2: "مدیریت شبکه",
    projectCategory3: "نرم‌افزار سازمانی",
    projectCategory4: "هوش مصنوعی",

    test1:
      "تفاوت اصلی این پروژه برای ما، شروع مدیریت دانش از مسئله‌های واقعی سازمان بود، نه از انتخاب ابزار و نرم‌افزار. تیم مشاور با شناخت دقیق فرایندها و چالش‌های سازمان، راهکارهایی متناسب با نیازهای ما طراحی و اجرا کرد.",

    test2:
      "یکی از نقاط قوت همکاری، رویکرد کاملاً اجرایی تیم مشاور بود. خروجی پروژه فقط مجموعه‌ای از مستندات نبود؛ بلکه فرایندها، نقش‌ها و سازوکارهایی ایجاد شد که امکان ادامه و توسعه مدیریت دانش را در سازمان فراهم می‌کند.",

    test3:
      "پیش از استفاده از سامانه، شناسایی منشأ اختلالات شبکه زمان زیادی از کارشناسان می‌گرفت. داشبوردها و اطلاعات متمرکز نرم‌افزار، فرآیند تشخیص و رفع مشکل را برای تیم ما بسیار سریع‌تر کرده است.",

    test4:
      "برای ما امنیت و کنترل داده‌ها اهمیت بالایی داشت. استفاده از یک راهکار بومی که امکان استقرار در زیرساخت سازمان را فراهم می‌کند، باعث شد بتوانیم مدیریت و پایش شبکه را بدون وابستگی به سرویس‌های خارجی انجام دهیم.",

    test5:
      "حجم بالای اسناد و اطلاعات سازمان باعث شده بود پیدا کردن اطلاعات موردنیاز زمان زیادی از کارشناسان بگیرد. موتور جستجو و دستیار هوشمند رایا این امکان را فراهم کرد که اطلاعات موردنیاز را سریع‌تر و دقیق‌تر از میان منابع مختلف سازمان پیدا کنیم.",

    test6:
      "مزیت اصلی موتور جستجوی رایا برای ما این است که جستجو فقط بر اساس تطابق کلمات انجام نمی‌شود؛ سیستم می‌تواند مفهوم و ارتباط محتوای موردنظر را نیز درک کند و نتایج مرتبط‌تری در اختیار کاربر قرار دهد.",

    role1: "رئیس سیستم‌های کیفیت و سرآمدی، شرکت فولاد مبارکه اصفهان",
    role2: "مدیر مهندسی صنایع، شرکت فولاد سنگان",

    role3: "رئیس فناوری اطلاعات، اداره کل کتابخانه‌های عمومی استان کرمانشاه",

    role4: "مدیر فناوری اطلاعات",
    role5: "مدیر دانش",
    role6: "کارشناس ارشد فناوری",

    phone1: "+۹۸-۲۱-۱۲۳۴۵۶۷۸",
    phone2: "+۹۸-۲۱-۷۶۵۴۳۲۱۰",

    email: "info@raybidpouye.com",

    aboutLink: "درباره ما",
    serviceLink1: "مشاوره مدیریت دانش",
    serviceLink2: "توسعه نرم‌افزارهای هوشمند",
    serviceLink3: "پیاده‌سازی سیستم‌های دانش",
    serviceLink4: "پشتیبانی و آموزش",
    resourceLink1: "مستندات",
    resourceLink2: "هوش مصنوعی",
    resourceLink3: "تحول دیجیتال",
  },
};

/* =========================================================
   NAVIGATION
========================================================= */

const navItems = [
  {
    id: "home",
    number: "01",
    label: {
      en: "Home",
      fa: "خانه",
    },
  },
  {
    id: "about",
    number: "02",
    label: {
      en: "About",
      fa: "درباره ما",
    },
  },
  {
    id: "services",
    number: "03",
    label: {
      en: "Services",
      fa: "خدمات",
    },
  },
  {
    id: "expertise",
    number: "04",
    label: {
      en: "Expertise",
      fa: "تخصص",
    },
  },
  {
    id: "testimonials",
    number: "05",
    label: {
      en: "Testimonials",
      fa: "نظرات",
    },
  },
  {
    id: "case-studies",
    number: "06",
    label: {
      en: "Projects",
      fa: "پروژه‌ها",
    },
  },
  {
    id: "contact",
    number: "07",
    label: {
      en: "Contact",
      fa: "تماس",
    },
  },
];

/* =========================================================
   SERVICES
========================================================= */

const services = [
  {
    number: "01",
    title: {
      en: "Intelligent Network Management Software",
      fa: "نرم‌افزار مدیریت هوشمند شبکه",
    },
    description: {
      en: "A comprehensive software for intelligent management and monitoring of organizational networks.",
      fa: "نرم‌افزاری جامع برای مدیریت و پایش هوشمند شبکه‌های سازمانی.",
    },
  },
  {
    number: "02",
    title: {
      en: "Intelligent Search Engine & GPT Assistant",
      fa: "موتور جستجوی هوشمند و دستیار GPT",
    },
    description: {
      en: "Fast access to organizational information through intelligent search and AI assistance.",
      fa: "دسترسی سریع به اطلاعات سازمان از طریق جستجوی هوشمند و دستیار هوش مصنوعی.",
    },
  },
  {
    number: "03",
    title: {
      en: "Raya Intelligent Knowledge Network",
      fa: "شبکه دانش هوشمند رایا",
    },
    description: {
      en: "A platform for managing, exchanging and developing knowledge in organizations.",
      fa: "بستری برای مدیریت، تبادل و توسعه دانش در سازمان.",
    },
  },
  {
    number: "04",
    title: {
      en: "Data Analytics Platform",
      fa: "سامانه تحلیل داده",
    },
    description: {
      en: "Advanced organizational analytics with accurate and interactive reports.",
      fa: "تحلیل پیشرفته داده‌های سازمانی با گزارش‌های دقیق و تعاملی.",
    },
  },
  {
    number: "05",
    title: {
      en: "Enterprise Integration Platform",
      fa: "پلتفرم یکپارچه سازمانی",
    },
    description: {
      en: "Connecting organizational systems and simplifying data flows.",
      fa: "اتصال سامانه‌های سازمانی و تسهیل جریان داده.",
    },
  },
  {
    number: "06",
    title: {
      en: "Network Security Solution",
      fa: "راهکار امنیت شبکه",
    },
    description: {
      en: "Threat detection, monitoring and rapid response for secure infrastructures.",
      fa: "شناسایی تهدیدات، پایش و واکنش سریع برای زیرساخت امن.",
    },
  },
];

/* =========================================================
   PROJECTS
========================================================= */

const projects = [
  {
    title: {
      en: "Mobarakeh Steel Knowledge Management Project",
      fa: "پروژه مدیریت دانش فولاد مبارکه",
    },
    category: {
      en: "Knowledge Management",
      fa: "مدیریت دانش",
    },
    image:
      "https://images.unsplash.com/photo-1497366754035-f200968a6e72?q=80&w=1200&auto=format&fit=crop",
    hue: 245,
  },
  {
    title: {
      en: "Sangan Steel Intelligent Network Project",
      fa: "پروژه شبکه هوشمند فولاد سنگان",
    },
    category: {
      en: "Network Management",
      fa: "مدیریت شبکه",
    },
    image:
      "https://images.unsplash.com/photo-1518005020951-eccb494ad742?q=80&w=1200&auto=format&fit=crop",
    hue: 210,
  },
  {
    title: {
      en: "Public Libraries Management System",
      fa: "سامانه مدیریت کتابخانه‌های عمومی",
    },
    category: {
      en: "Enterprise Software",
      fa: "نرم‌افزار سازمانی",
    },
    image:
      "https://images.unsplash.com/photo-1497366811353-6870744d04b2?q=80&w=1200&auto=format&fit=crop",
    hue: 275,
  },
  {
    title: {
      en: "Enterprise Search Engine",
      fa: "موتور جستجوی سازمانی",
    },
    category: {
      en: "Artificial Intelligence",
      fa: "هوش مصنوعی",
    },
    image:
      "https://images.unsplash.com/photo-1559028012-481c04fa702d?q=80&w=1200&auto=format&fit=crop",
    hue: 190,
  },
];

/* =========================================================
   EXPERTISE
========================================================= */

const expertiseTags = [
  "Marketing",
  "SEO",
  "Social Media",
  "Web Development",
  "UI Design",
  "Mobile Apps",
  "Photography",
  "Company Profile",
  "Visual Editing",
];

const activeExpertiseTags = ["Web Development", "UI Design", "Mobile Apps"];

/* =========================================================
   TESTIMONIALS
========================================================= */

const testimonials = [
  {
    name: "مهندس علی کیانی",
    role: {
      en: "Head of Quality and Excellence Systems, Mobarakeh Steel Company",
      fa: "رئیس سیستم‌های کیفیت و سرآمدی، شرکت فولاد مبارکه اصفهان",
    },
    text: {
      en: translations.en.test1,
      fa: translations.fa.test1,
    },
    rating: 5,
    image: "https://i.pravatar.cc/150?img=12",
  },
  {
    name: "مهندس رضا صادقی",
    role: {
      en: "Industrial Engineering Manager, Sangan Steel Company",
      fa: "مدیر مهندسی صنایع، شرکت فولاد سنگان",
    },
    text: {
      en: translations.en.test2,
      fa: translations.fa.test2,
    },
    rating: 5,
    image: "https://i.pravatar.cc/150?img=11",
  },
  {
    name: "دکتر آرین مطاعی",
    role: {
      en: "IT Director, General Directorate of Public Libraries of Kermanshah Province",
      fa: "رئیس فناوری اطلاعات، اداره کل کتابخانه‌های عمومی استان کرمانشاه",
    },
    text: {
      en: translations.en.test3,
      fa: translations.fa.test3,
    },
    rating: 5,
    image: "https://i.pravatar.cc/150?img=47",
  },
  {
    name: "مدیر فناوری اطلاعات",
    role: {
      en: "IT Manager",
      fa: "مدیر فناوری اطلاعات",
    },
    text: {
      en: translations.en.test4,
      fa: translations.fa.test4,
    },
    rating: 5,
    image: "https://i.pravatar.cc/150?img=32",
  },
  {
    name: "مدیر دانش",
    role: {
      en: "Knowledge Manager",
      fa: "مدیر دانش",
    },
    text: {
      en: translations.en.test5,
      fa: translations.fa.test5,
    },
    rating: 5,
    image: "https://i.pravatar.cc/150?img=53",
  },
  {
    name: "کارشناس ارشد فناوری",
    role: {
      en: "Senior Technology Expert",
      fa: "کارشناس ارشد فناوری",
    },
    text: {
      en: translations.en.test6,
      fa: translations.fa.test6,
    },
    rating: 5,
    image: "https://i.pravatar.cc/150?img=45",
  },
];

/* =========================================================
   STATS
========================================================= */

const stats = [
  {
    key: "experience",
    target: 16,
    suffix: "+",
    label: {
      en: "YEARS EXPERIENCE",
      fa: "سال تجربه",
    },
  },
  {
    key: "projects",
    target: 50,
    suffix: "+",
    label: {
      en: "PROJECTS DELIVERED",
      fa: "پروژه موفق",
    },
  },
  {
    key: "clients",
    target: 19,
    suffix: "+",
    label: {
      en: "ORGANIZATIONS",
      fa: "سازمان",
    },
  },
];

const aboutStats = stats;

const animatedStats = reactive({
  experience: 0,
  projects: 0,
  clients: 0,
});

/* =========================================================
   CONTACT
========================================================= */

const contactData = {
  phone1Raw: "+982112345678",
  phone2Raw: "+982176543210",
  email: "info@raybidpouye.com",
};

/* =========================================================
   FOOTER
========================================================= */

const footerColumns = [
  {
    key: "company",
    title: "footer.COMPANY",
    links: [
      { label: "aboutLink", href: "#about" },
      { label: "serviceLink1", href: "#services" },
      { label: "serviceLink2", href: "#services" },
    ],
  },
  {
    key: "services",
    title: "footer.SERVICES",
    links: [
      { label: "serviceLink1", href: "#services" },
      { label: "serviceLink2", href: "#services" },
      { label: "serviceLink3", href: "#services" },
      { label: "serviceLink4", href: "#contact" },
    ],
  },
  {
    key: "resources",
    title: "footer.RESOURCES",
    links: [
      { label: "resourceLink1", href: "#contact" },
      { label: "resourceLink2", href: "#expertise" },
      { label: "resourceLink3", href: "#case-studies" },
    ],
  },
];

/* =========================================================
   HELPERS
========================================================= */

const t = (path) => {
  const parts = path.split(".");

  let value = translations[language.value];

  for (const part of parts) {
    value = value?.[part];
  }

  return value ?? "";
};

/* =========================================================
   SEO
========================================================= */

const setMeta = (key, content) => {
  const isProperty = key.startsWith("og:") || key.startsWith("twitter:");

  const attribute = isProperty ? "property" : "name";

  let element = document.head.querySelector(`meta[${attribute}="${key}"]`);

  if (!element) {
    element = document.createElement("meta");

    element.setAttribute(attribute, key);

    document.head.appendChild(element);
  }

  element.setAttribute("content", content);
};

const updateSeo = () => {
  if (typeof document === "undefined") {
    return;
  }

  const isFa = language.value === "fa";

  document.documentElement.lang = isFa ? "fa" : "en";
  document.documentElement.dir = isFa ? "rtl" : "ltr";

  document.title = isFa
    ? "رایبد پویه | راهکارهای هوشمند نرم‌افزاری و سازمانی"
    : "Raybod Pouye | Intelligent Software & Digital Solutions";

  const description = isFa
    ? "رایبد پویه در زمینه تولید نرم‌افزارهای هوشمند، هوش مصنوعی، مدیریت دانش، مدیریت شبکه، تحلیل داده، یکپارچه‌سازی سازمانی و امنیت شبکه فعالیت می‌کند."
    : "Raybod Pouye provides intelligent software, AI, knowledge management, network management, data analytics, enterprise integration and network security solutions.";

  setMeta("description", description);
  setMeta("robots", "index, follow");
  setMeta("author", "Raybod Pouye");

  setMeta("og:type", "website");
  setMeta("og:title", document.title);
  setMeta("og:description", description);
  setMeta("og:url", window.location.href);
  setMeta("og:site_name", "Raybod Pouye");
  setMeta("og:locale", isFa ? "fa_IR" : "en_US");

  setMeta("twitter:card", "summary");
  setMeta("twitter:title", document.title);
  setMeta("twitter:description", description);

  let schema = document.getElementById("raybod-jsonld");

  const json = {
    "@context": "https://schema.org",

    "@graph": [
      {
        "@type": "Organization",
        name: isFa ? "رایبد پویه" : "Raybod Pouye",
        url: window.location.origin,
        email: contactData.email,
        description,
      },
      {
        "@type": "WebSite",
        name: document.title,
        url: window.location.origin,
        inLanguage: isFa ? "fa" : "en",
      },
    ],
  };

  if (!schema) {
    schema = document.createElement("script");

    schema.id = "raybod-jsonld";
    schema.type = "application/ld+json";

    document.head.appendChild(schema);
  }

  schema.textContent = JSON.stringify(json);
};

/* =========================================================
   LANGUAGE
========================================================= */

const changeLanguage = async (nextLanguage) => {
  if (nextLanguage !== "fa" && nextLanguage !== "en") {
    return;
  }

  language.value = nextLanguage;

  localStorage.setItem("raybod-language", nextLanguage);

  await nextTick();

  updateSeo();
};

const toggleLanguage = async () => {
  await changeLanguage(language.value === "en" ? "fa" : "en");
};

/* =========================================================
   NAVIGATION
========================================================= */

const setActive = (sectionId) => {
  activeSection.value = sectionId;
};

const toggleMobileMenu = () => {
  mobileMenuOpen.value = !mobileMenuOpen.value;

  document.body.classList.toggle("menu-lock", mobileMenuOpen.value);
};

const closeMobileMenu = () => {
  mobileMenuOpen.value = false;

  document.body.classList.remove("menu-lock");
};

/* =========================================================
   FOOTER
========================================================= */

const toggleFooterSection = (section) => {
  openFooterSection.value =
    openFooterSection.value === section ? null : section;
};

/* =========================================================
   SCROLL
========================================================= */

const handleScroll = () => {
  scrolled.value = window.scrollY > 18;
};

/* =========================================================
   SECTION OBSERVER
========================================================= */

const setupSectionObserver = () => {
  const sections = navItems
    .map((item) => document.getElementById(item.id))
    .filter(Boolean);

  sectionObserver = new IntersectionObserver(
    (entries) => {
      const visible = entries
        .filter((entry) => entry.isIntersecting)
        .sort((a, b) => b.intersectionRatio - a.intersectionRatio);

      if (visible[0]) {
        activeSection.value = visible[0].target.id;
      }
    },
    {
      threshold: [0.15, 0.35, 0.6],
      rootMargin: "-20% 0px -55% 0px",
    },
  );

  sections.forEach((section) => sectionObserver.observe(section));
};

/* =========================================================
   REVEAL
========================================================= */

const setupRevealObserver = () => {
  const items = document.querySelectorAll(".reveal:not(.is-visible)");

  revealObserver = new IntersectionObserver(
    (entries) => {
      entries.forEach((entry) => {
        if (!entry.isIntersecting) {
          return;
        }

        entry.target.classList.add("is-visible");

        revealObserver?.unobserve(entry.target);
      });
    },
    {
      threshold: 0.1,
      rootMargin: "0px 0px -40px",
    },
  );

  items.forEach((item) => revealObserver.observe(item));
};

/* =========================================================
   COUNTERS
========================================================= */

const animateCounters = () => {
  const start = performance.now();

  const duration = 1500;

  cancelAnimationFrame(statsAnimationFrame);

  const tick = (now) => {
    const progress = Math.min((now - start) / duration, 1);

    const eased = 1 - Math.pow(1 - progress, 3);

    stats.forEach((stat) => {
      animatedStats[stat.key] = Math.round(stat.target * eased);
    });

    if (progress < 1) {
      statsAnimationFrame = requestAnimationFrame(tick);
    }
  };

  statsAnimationFrame = requestAnimationFrame(tick);
};

/* =========================================================
   SCROLL TOP
========================================================= */

const scrollTop = () => {
  window.scrollTo({
    top: 0,
    behavior: "smooth",
  });
};

/* =========================================================
   LIFECYCLE
========================================================= */

onMounted(async () => {
  const savedLanguage = localStorage.getItem("raybod-language");

  if (savedLanguage === "fa" || savedLanguage === "en") {
    language.value = savedLanguage;
  }

  updateSeo();

  window.addEventListener("scroll", handleScroll, { passive: true });

  handleScroll();

  await nextTick();

  setupRevealObserver();
  setupSectionObserver();

  window.setTimeout(() => {
    animateCounters();
  }, 450);

  document.body.classList.add("page-is-loading");

  loadingTimer = window.setTimeout(() => {
    isLoading.value = false;

    document.body.classList.remove("page-is-loading");
  }, 2500);
});

onBeforeUnmount(() => {
  window.removeEventListener("scroll", handleScroll);

  if (loadingTimer) {
    window.clearTimeout(loadingTimer);
  }

  revealObserver?.disconnect();
  sectionObserver?.disconnect();

  cancelAnimationFrame(statsAnimationFrame);

  document.body.classList.remove("menu-lock");

  document.body.classList.remove("page-is-loading");
});
</script>

<style>
/* =========================================================
   01. FONTS & VARIABLES
========================================================= */

@import url("https://fonts.googleapis.com/css2?family=DM+Serif+Display:ital@0;1&family=Inter:wght@400;500;600;700&family=Vazirmatn:wght@400;500;600;700;800&display=swap");

:root {
  --page-bg: #f6f6f8;
  --page-bg-2: #f0f0f4;
  --white: #fff;

  --ink: #111723;
  --ink-soft: #4a5262;
  --muted: #89919f;
  --muted-2: #a3a9b4;

  --line: rgba(37, 45, 60, 0.12);

  --accent: #8479f4;
  --accent-light: #c8c1ff;
  --accent-blue: #b6d3ff;

  --container: 1240px;

  font-family: "Inter", sans-serif;
  font-synthesis: none;
  text-rendering: optimizeLegibility;
  -webkit-font-smoothing: antialiased;
}

*,
*::before,
*::after {
  box-sizing: border-box;
}

html {
  scroll-behavior: smooth;
  background: var(--page-bg);
}

body {
  width: 100%;
  min-width: 320px;
  margin: 0;
  background: var(--page-bg);
  color: var(--ink);
}

body,
button,
a {
  font-family: inherit;
}

button,
input,
textarea,
select {
  font: inherit;
}

button {
  border: 0;
}

a {
  color: inherit;
  text-decoration: none;
}

img {
  display: block;
  max-width: 100%;
}

::selection {
  color: #fff;
  background: var(--accent);
}

body.menu-lock,
body.page-is-loading {
  overflow: hidden;
}

:where(a, button, select):focus-visible {
  outline: 2px solid rgba(132, 121, 244, 0.65);
  outline-offset: 4px;
}

/* =========================================================
   02. GLOBAL
========================================================= */

html,
body,
#app,
.site-shell {
  width: 100%;
  min-width: 320px;
  max-width: none !important;
  margin: 0;
  padding-left: 0;
  padding-right: 0;
  border: 0 !important;
  outline: 0 !important;
}

.site-shell {
  position: relative;
  min-height: 100vh;
  overflow-x: clip;

  background:
    radial-gradient(
      circle at 82% 12%,
      rgba(203, 212, 255, 0.22),
      transparent 26%
    ),
    var(--page-bg);
}

.container {
  width: min(calc(100% - 64px), var(--container));
  margin-inline: auto;
}

.section {
  position: relative;
}

.desktop-only {
  display: inline-flex;
}

/* =========================================================
   03. PREMIUM LIQUID ORB LOADER
========================================================= */

.page-loader {
  position: fixed;
  inset: 0;
  z-index: 5000;

  display: grid;
  place-items: center;

  overflow: hidden;
  isolation: isolate;

  background:
    radial-gradient(
      circle at 50% 48%,
      rgba(220, 218, 255, 0.62),
      transparent 22%
    ),
    radial-gradient(
      circle at 18% 78%,
      rgba(137, 119, 255, 0.1),
      transparent 25%
    ),
    radial-gradient(
      circle at 82% 22%,
      rgba(114, 195, 255, 0.11),
      transparent 27%
    ),
    linear-gradient(135deg, #fafafd 0%, #f1f1f7 48%, #f8f8fb 100%);
}

.loader-atmosphere {
  position: absolute;
  inset: -25%;

  background:
    radial-gradient(
      circle at 26% 75%,
      rgba(136, 120, 255, 0.12),
      transparent 20%
    ),
    radial-gradient(
      circle at 74% 28%,
      rgba(99, 186, 255, 0.11),
      transparent 22%
    ),
    radial-gradient(
      circle at 50% 50%,
      rgba(255, 255, 255, 0.5),
      transparent 28%
    );

  filter: blur(55px);

  animation: loaderAtmosphereMove 6s ease-in-out infinite;
}

.loader-glow {
  position: absolute;

  width: 340px;
  height: 340px;

  border-radius: 50%;

  filter: blur(95px);

  pointer-events: none;
}

.loader-glow-1 {
  left: 4%;
  bottom: 4%;

  background: rgba(124, 107, 255, 0.85);

  opacity: 0.14;

  animation: loaderGlowLeft 5.5s ease-in-out infinite;
}

.loader-glow-2 {
  right: 3%;
  top: 8%;

  background: rgba(84, 184, 255, 0.8);

  opacity: 0.12;

  animation: loaderGlowRight 6s ease-in-out infinite;
}

.loader-glow-3 {
  left: 50%;
  top: 50%;

  width: 220px;
  height: 220px;

  transform: translate(-50%, -50%);

  background: rgba(136, 122, 255, 0.8);

  opacity: 0.13;

  filter: blur(75px);

  animation: loaderCenterGlow 4s ease-in-out infinite;
}

/* =========================================================
   PARTICLES
========================================================= */

.loader-particles {
  position: absolute;
  inset: 0;

  overflow: hidden;
  pointer-events: none;
}

.loader-particles span {
  position: absolute;

  left: calc(5% + (var(--i, 0) * 5.2%));

  top: calc(8% + (var(--i, 0) * 4.7%));

  width: 3px;
  height: 3px;

  border-radius: 50%;

  background: rgba(255, 255, 255, 0.75);

  box-shadow:
    0 0 10px rgba(155, 147, 255, 0.55),
    0 0 22px rgba(155, 147, 255, 0.18);

  opacity: 0;

  animation:
    particleFloat 4.5s ease-in-out infinite,
    particleAppear 2s ease forwards;
}

.loader-particles span:nth-child(1) {
  --i: 1;
  animation-delay: 0.1s;
}

.loader-particles span:nth-child(2) {
  --i: 2;
  animation-delay: 0.35s;
}

.loader-particles span:nth-child(3) {
  --i: 3;
  animation-delay: 0.6s;
}

.loader-particles span:nth-child(4) {
  --i: 4;
  animation-delay: 0.9s;
}

.loader-particles span:nth-child(5) {
  --i: 5;
  animation-delay: 1.1s;
}

.loader-particles span:nth-child(6) {
  --i: 6;
  animation-delay: 1.35s;
}

.loader-particles span:nth-child(7) {
  --i: 7;
  animation-delay: 1.6s;
}

.loader-particles span:nth-child(8) {
  --i: 8;
  animation-delay: 1.85s;
}

.loader-particles span:nth-child(9) {
  --i: 9;
  animation-delay: 2.1s;
}

.loader-particles span:nth-child(10) {
  --i: 10;
  animation-delay: 2.3s;
}

.loader-particles span:nth-child(11) {
  --i: 11;
  animation-delay: 2.5s;
}

.loader-particles span:nth-child(12) {
  --i: 12;
  animation-delay: 2.7s;
}

.loader-particles span:nth-child(13) {
  --i: 13;
  animation-delay: 2.9s;
}

.loader-particles span:nth-child(14) {
  --i: 14;
  animation-delay: 3.1s;
}

.loader-particles span:nth-child(15) {
  --i: 15;
  animation-delay: 3.3s;
}

.loader-particles span:nth-child(16) {
  --i: 16;
  animation-delay: 3.5s;
}

.loader-particles span:nth-child(17) {
  --i: 17;
  animation-delay: 3.7s;
}

.loader-particles span:nth-child(18) {
  --i: 18;
  animation-delay: 3.9s;
}

/* =========================================================
   BUBBLES
========================================================= */

.loader-bubble-field {
  position: absolute;
  inset: 0;
  overflow: hidden;
}

.loader-bubble {
  position: absolute;

  left: var(--x);
  top: 0;

  width: var(--size);
  height: var(--size);

  border-radius: 50%;

  opacity: 0;

  transform: translate3d(-50%, calc(100vh + var(--size)), 0) scale(0.58);

  background: radial-gradient(
    circle at 26% 18%,
    rgba(255, 255, 255, 1) 0 7%,
    hsla(var(--hue), 100%, 96%, 0.98) 17%,
    hsla(var(--hue), 90%, 80%, 0.76) 43%,
    hsla(calc(var(--hue) + 28), 90%, 77%, 0.3) 72%,
    rgba(255, 255, 255, 0.03) 100%
  );

  border: 1px solid rgba(255, 255, 255, 0.86);

  box-shadow:
    inset 10px 9px 18px rgba(255, 255, 255, 0.7),
    inset -12px -14px 25px rgba(66, 77, 164, 0.13),
    0 20px 55px rgba(88, 96, 186, 0.16),
    0 0 26px hsla(var(--hue), 90%, 80%, 0.12);

  will-change: transform, opacity;

  animation: bubbleRise var(--rise) cubic-bezier(0.16, 0.85, 0.22, 1)
    var(--delay) forwards;
}

.loader-bubble-1 {
  --target-y: 31vh;
  --drift: -34px;
  --rotation: -8deg;
}

.loader-bubble-2 {
  --target-y: 43vh;
  --drift: 25px;
  --rotation: 9deg;
}

.loader-bubble-3 {
  --target-y: 25vh;
  --drift: -12px;
  --rotation: -5deg;
}

.loader-bubble-4 {
  --target-y: 38vh;
  --drift: 35px;
  --rotation: 8deg;
}

.loader-bubble-5 {
  --target-y: 50vh;
  --drift: -21px;
  --rotation: -10deg;
}

.loader-bubble-6 {
  --target-y: 29vh;
  --drift: 19px;
  --rotation: 6deg;
}

.bubble-shine {
  position: absolute;

  left: 17%;
  top: 13%;

  width: 27%;
  height: 15%;

  border-radius: 50%;

  background: rgba(255, 255, 255, 0.9);

  filter: blur(4px);

  transform: rotate(-22deg);
}

.bubble-inner-glow {
  position: absolute;

  inset: 7%;

  border-radius: 50%;

  border: 1px solid rgba(255, 255, 255, 0.22);

  opacity: 0.65;

  animation: bubbleInnerGlow 2s ease-in-out infinite;
}

/* =========================================================
   CENTRAL SYSTEM
========================================================= */

.loader-system {
  position: relative;
  z-index: 20;

  width: 250px;
  height: 250px;

  display: grid;
  place-items: center;

  transform: translateZ(0);
}

.loader-system::before {
  position: absolute;
  content: "";

  width: 220px;
  height: 220px;

  border-radius: 50%;

  border: 1px solid rgba(132, 121, 244, 0.08);

  box-shadow:
    0 0 40px rgba(132, 121, 244, 0.07),
    inset 0 0 40px rgba(255, 255, 255, 0.15);

  animation: systemPulse 3s ease-in-out infinite;
}

.loader-orbit {
  position: absolute;

  left: 50%;
  top: 50%;

  border-radius: 50%;

  pointer-events: none;
}

.loader-orbit-1 {
  width: 205px;
  height: 84px;

  border: 1px solid rgba(127, 117, 239, 0.22);

  transform: translate(-50%, -50%) rotate(28deg);

  animation: orbitSpinOne 6s linear infinite;
}

.loader-orbit-2 {
  width: 175px;
  height: 68px;

  border: 1px solid rgba(89, 173, 241, 0.2);

  transform: translate(-50%, -50%) rotate(-34deg);

  animation: orbitSpinTwo 7.5s linear infinite;
}

.loader-orbit-3 {
  width: 235px;
  height: 100px;

  border: 1px solid rgba(255, 255, 255, 0.5);

  transform: translate(-50%, -50%) rotate(72deg);

  animation: orbitSpinThree 10s linear infinite;
}

.loader-orbit-dot {
  position: absolute;

  left: 50%;
  top: 50%;

  border-radius: 50%;

  background: #fff;

  box-shadow:
    0 0 8px rgba(141, 132, 255, 0.65),
    0 0 22px rgba(141, 132, 255, 0.28);
}

.loader-orbit-dot-1 {
  width: 6px;
  height: 6px;

  transform: translate(-50%, -50%) translateX(103px);

  animation: orbitDotOne 6s linear infinite;
}

.loader-orbit-dot-2 {
  width: 4px;
  height: 4px;

  transform: translate(-50%, -50%) translateX(-88px);

  animation: orbitDotTwo 7.5s linear infinite;
}

.loader-orbit-dot-3 {
  width: 5px;
  height: 5px;

  transform: translate(-50%, -50%) translateY(-118px);

  animation: orbitDotThree 10s linear infinite;
}

/* =========================================================
   CORE
========================================================= */

.loader-core {
  position: relative;
  z-index: 10;

  width: 82px;
  height: 82px;

  border-radius: 50%;

  background: radial-gradient(
    circle at 28% 22%,
    #ffffff 0 7%,
    #eeedff 18%,
    #d2ceff 36%,
    #afa8f1 62%,
    #93a9ea 86%,
    rgba(255, 255, 255, 0.25)
  );

  border: 1px solid rgba(255, 255, 255, 0.92);

  box-shadow:
    inset 10px 9px 20px rgba(255, 255, 255, 0.88),
    inset -10px -12px 23px rgba(75, 82, 174, 0.17),
    0 18px 45px rgba(105, 96, 212, 0.2),
    0 0 50px rgba(132, 121, 244, 0.14);

  animation: loaderCoreFloat 3s ease-in-out infinite;
}

.loader-core-glow {
  position: absolute;
  inset: -20px;

  border-radius: 50%;

  border: 1px solid rgba(140, 130, 255, 0.14);

  box-shadow:
    0 0 40px rgba(132, 121, 244, 0.11),
    inset 0 0 25px rgba(132, 121, 244, 0.05);

  animation: loaderCorePulse 2.8s ease-in-out infinite;
}

.loader-core-inner {
  position: absolute;

  inset: 17px;

  border-radius: 50%;

  border: 1px solid rgba(255, 255, 255, 0.5);

  background: radial-gradient(
    circle at 35% 30%,
    rgba(255, 255, 255, 0.88),
    rgba(201, 196, 255, 0.44) 45%,
    rgba(127, 139, 229, 0.18)
  );

  box-shadow:
    inset 4px 4px 9px rgba(255, 255, 255, 0.65),
    inset -4px -5px 9px rgba(89, 94, 172, 0.12);

  animation: coreInnerPulse 2s ease-in-out infinite;
}

.loader-core-highlight {
  position: absolute;

  left: 20px;
  top: 16px;

  width: 22px;
  height: 12px;

  border-radius: 50%;

  background: rgba(255, 255, 255, 0.58);

  filter: blur(5px);

  transform: rotate(-28deg);

  animation: coreHighlight 2.8s ease-in-out infinite;
}

/* =========================================================
   LABEL
========================================================= */

.loader-label {
  position: absolute;
  z-index: 30;

  left: 50%;
  bottom: 48px;

  display: flex;
  align-items: center;

  gap: 11px;

  color: #7d8595;

  font-size: 9px;
  letter-spacing: 0.16em;

  transform: translateX(-50%);

  animation: loaderLabelIn 0.9s 0.35s cubic-bezier(0.22, 1, 0.36, 1) both;
}

.loader-label i {
  width: 28px;
  height: 1px;

  background: #b9bec8;

  animation: loaderLinePulse 1.8s ease-in-out infinite;
}

.loader-label strong {
  color: #6f69c9;

  font-size: 10px;
  font-weight: 700;

  letter-spacing: 0.08em;
}

/* =========================================================
   EXIT
========================================================= */

.loader-leave-active {
  pointer-events: none;

  transition:
    opacity 0.9s ease,
    transform 0.9s cubic-bezier(0.22, 1, 0.36, 1);
}

.loader-leave-to {
  opacity: 0;
  transform: scale(1.035);
}

.loader-leave-to .loader-system {
  animation: systemExit 0.8s cubic-bezier(0.16, 1, 0.3, 1) forwards;
}

.loader-leave-to .loader-core {
  animation: coreExplosion 0.78s cubic-bezier(0.16, 1, 0.3, 1) forwards;
}

.loader-leave-to .loader-bubble {
  animation: bubbleExplosion 0.72s cubic-bezier(0.16, 1, 0.3, 1) forwards;
}

.loader-leave-to .loader-orbit {
  animation: orbitExplosion 0.75s cubic-bezier(0.16, 1, 0.3, 1) forwards;
}

/* =========================================================
   KEYFRAMES
========================================================= */

@keyframes loaderAtmosphereMove {
  0%,
  100% {
    transform: scale(0.96) translate3d(0, 0, 0);
    opacity: 0.7;
  }

  50% {
    transform: scale(1.05) translate3d(1%, -1%, 0);
    opacity: 1;
  }
}

@keyframes loaderGlowLeft {
  0%,
  100% {
    transform: translate3d(0, 0, 0) scale(0.9);
  }

  50% {
    transform: translate3d(30px, -20px, 0) scale(1.12);
  }
}

@keyframes loaderGlowRight {
  0%,
  100% {
    transform: translate3d(0, 0, 0) scale(0.92);
  }

  50% {
    transform: translate3d(-28px, 22px, 0) scale(1.1);
  }
}

@keyframes loaderCenterGlow {
  0%,
  100% {
    transform: translate(-50%, -50%) scale(0.88);
    opacity: 0.55;
  }

  50% {
    transform: translate(-50%, -50%) scale(1.12);
    opacity: 0.95;
  }
}

@keyframes particleAppear {
  from {
    opacity: 0;
  }

  to {
    opacity: 0.75;
  }
}

@keyframes particleFloat {
  0%,
  100% {
    transform: translate3d(0, 0, 0) scale(0.8);
  }

  50% {
    transform: translate3d(8px, -15px, 0) scale(1.15);
  }
}

@keyframes bubbleRise {
  0% {
    opacity: 0;

    transform: translate3d(-50%, calc(100vh + var(--size)), 0) scale(0.58);
  }

  10% {
    opacity: 0.5;
  }

  31% {
    transform: translate3d(calc(-50% + var(--drift)), 72vh, 0) scale(0.8)
      rotate(calc(var(--rotation) * 0.45));
  }

  54% {
    opacity: 1;

    transform: translate3d(calc(-50% - var(--drift)), 48vh, 0) scale(0.95)
      rotate(calc(var(--rotation) * -0.5));
  }

  72% {
    transform: translate3d(
        calc(-50% + var(--drift)),
        calc(var(--target-y) + 16px),
        0
      )
      scale(1.04) rotate(var(--rotation));
  }

  87% {
    transform: translate3d(calc(-50% - 7px), calc(var(--target-y) - 4px), 0)
      scale(0.98);
  }

  100% {
    opacity: 1;

    transform: translate3d(-50%, var(--target-y), 0) scale(1);
  }
}

@keyframes bubbleInnerGlow {
  0%,
  100% {
    opacity: 0.3;
    transform: scale(0.92);
  }

  50% {
    opacity: 0.85;
    transform: scale(1.04);
  }
}

@keyframes systemPulse {
  0%,
  100% {
    transform: scale(0.95);
    opacity: 0.5;
  }

  50% {
    transform: scale(1.06);
    opacity: 1;
  }
}

@keyframes loaderCoreFloat {
  0%,
  100% {
    transform: translate3d(0, 3px, 0) scale(0.97);
  }

  50% {
    transform: translate3d(0, -8px, 0) scale(1.04);
  }
}

@keyframes loaderCorePulse {
  0%,
  100% {
    opacity: 0.22;
    transform: scale(0.9);
  }

  50% {
    opacity: 0.72;
    transform: scale(1.08);
  }
}

@keyframes coreInnerPulse {
  0%,
  100% {
    transform: scale(0.94);
    opacity: 0.7;
  }

  50% {
    transform: scale(1.04);
    opacity: 1;
  }
}

@keyframes coreHighlight {
  0%,
  100% {
    opacity: 0.4;

    transform: translate3d(0, 0, 0) rotate(-28deg);
  }

  50% {
    opacity: 0.85;

    transform: translate3d(2px, -2px, 0) rotate(-20deg);
  }
}

@keyframes orbitSpinOne {
  from {
    transform: translate(-50%, -50%) rotate(28deg) rotateX(0deg);
  }

  to {
    transform: translate(-50%, -50%) rotate(28deg) rotateX(360deg);
  }
}

@keyframes orbitSpinTwo {
  from {
    transform: translate(-50%, -50%) rotate(-34deg) rotateY(0deg);
  }

  to {
    transform: translate(-50%, -50%) rotate(-34deg) rotateY(360deg);
  }
}

@keyframes orbitSpinThree {
  from {
    transform: translate(-50%, -50%) rotate(72deg);
  }

  to {
    transform: translate(-50%, -50%) rotate(432deg);
  }
}

@keyframes orbitDotOne {
  from {
    transform: translate(-50%, -50%) rotate(0deg) translateX(103px);
  }

  to {
    transform: translate(-50%, -50%) rotate(360deg) translateX(103px);
  }
}

@keyframes orbitDotTwo {
  from {
    transform: translate(-50%, -50%) rotate(0deg) translateX(-88px);
  }

  to {
    transform: translate(-50%, -50%) rotate(-360deg) translateX(-88px);
  }
}

@keyframes orbitDotThree {
  from {
    transform: translate(-50%, -50%) rotate(0deg) translateY(-118px);
  }

  to {
    transform: translate(-50%, -50%) rotate(360deg) translateY(-118px);
  }
}

@keyframes loaderLabelIn {
  from {
    opacity: 0;

    transform: translateX(-50%) translateY(14px);
  }

  to {
    opacity: 1;

    transform: translateX(-50%) translateY(0);
  }
}

@keyframes loaderLinePulse {
  0%,
  100% {
    width: 20px;
    opacity: 0.45;
  }

  50% {
    width: 34px;
    opacity: 1;
  }
}

@keyframes bubbleExplosion {
  0% {
    opacity: 1;

    transform: translate3d(-50%, var(--target-y), 0) scale(1);
  }

  35% {
    transform: translate3d(-50%, var(--target-y), 0) scale(1.26);
  }

  62% {
    opacity: 0.65;

    transform: translate3d(-50%, var(--target-y), 0) scale(1.65);
  }

  100% {
    opacity: 0;

    transform: translate3d(-50%, var(--target-y), 0) scale(2.15);

    filter: blur(10px);
  }
}

@keyframes coreExplosion {
  0% {
    opacity: 1;
    transform: scale(1);
  }

  55% {
    opacity: 0.8;
    transform: scale(1.4);
  }

  100% {
    opacity: 0;
    transform: scale(2.05);
    filter: blur(10px);
  }
}

@keyframes systemExit {
  0% {
    opacity: 1;
    transform: scale(1);
  }

  100% {
    opacity: 0;
    transform: scale(1.3);
    filter: blur(9px);
  }
}

@keyframes orbitExplosion {
  0% {
    opacity: 1;
  }

  100% {
    opacity: 0;

    transform: translate(-50%, -50%) scale(1.45) rotate(90deg);
  }
}

/* =========================================================
   04. HEADER
========================================================= */

.site-header {
  position: fixed;
  z-index: 1000;

  top: 0;
  left: 0;

  width: 100%;

  padding: 28px 0;

  transition:
    padding 0.35s ease,
    background 0.35s ease,
    backdrop-filter 0.35s ease;
}

.site-shell.scrolled .site-header {
  padding: 15px 0;

  background: rgba(246, 246, 248, 0.78);

  backdrop-filter: blur(18px);
  -webkit-backdrop-filter: blur(18px);

  box-shadow: 0 1px 0 rgba(20, 26, 38, 0.035);
}

.header-inner {
  display: flex;
  align-items: center;
  justify-content: space-between;
}

.brand {
  display: inline-flex;
  align-items: center;

  gap: 11px;

  flex-shrink: 0;
}

.brand-name {
  color: #171c27;

  letter-spacing: 0.16em;

  font-size: 13px;
  font-weight: 600;

  white-space: nowrap;
}

.brand-mark {
  position: relative;

  width: 22px;
  height: 22px;

  flex: 0 0 22px;

  transform: translateY(-7px);
}

.brand-mark i {
  position: absolute;

  left: 50%;
  top: 50%;

  width: 3px;
  height: 8px;

  border-radius: 8px;

  background: #151a24;

  transform-origin: center 12px;
}

.brand-mark i:nth-child(1) {
  transform: translate(-50%, -50%) rotate(0deg);
}

.brand-mark i:nth-child(2) {
  transform: translate(-50%, -50%) rotate(60deg);
}

.brand-mark i:nth-child(3) {
  transform: translate(-50%, -50%) rotate(120deg);
}

.brand-mark i:nth-child(4) {
  transform: translate(-50%, -50%) rotate(180deg);
}

.brand-mark i:nth-child(5) {
  transform: translate(-50%, -50%) rotate(240deg);
}

.brand-mark i:nth-child(6) {
  transform: translate(-50%, -50%) rotate(300deg);
}

.desktop-nav {
  position: absolute;

  left: 50%;

  display: flex;
  align-items: center;

  gap: 25px;

  transform: translateX(-50%);
}

.desktop-nav a {
  position: relative;

  padding: 7px 0;

  color: #838a98;

  font-size: 12px;

  white-space: nowrap;

  transition: color 0.25s ease;
}

.lang-fa .desktop-nav a {
  font-size: 14px;
  font-weight: 500;
}

.desktop-nav a::after {
  position: absolute;
  content: "";

  left: 0;
  right: 0;
  bottom: -5px;

  height: 1.5px;

  background: var(--accent);

  transform: scaleX(0);

  transition: transform 0.3s ease;
}

.desktop-nav a:hover,
.desktop-nav a.active {
  color: var(--ink);
}

.desktop-nav a.active::after {
  transform: scaleX(1);
}

.header-actions {
  display: flex;
  align-items: center;

  gap: 18px;

  flex-shrink: 0;
}

.language-switch {
  display: inline-flex;
  align-items: center;

  gap: 4px;

  padding: 0;

  color: #9aa0ab;

  background: none;

  cursor: pointer;

  font-size: 10px;

  letter-spacing: 0.1em;
}

.language-switch span.active {
  color: #1c2431;
}

.language-separator {
  color: #c0c4cb;
}

.talk-button {
  display: inline-flex;
  align-items: center;

  gap: 13px;

  height: 34px;

  padding: 0 13px 0 18px;

  border: 1px solid #bbc0c9;
  border-radius: 999px;

  color: #1d2430;

  font-size: 11px;

  white-space: nowrap;

  transition:
    transform 0.3s ease,
    border-color 0.3s ease,
    background 0.3s ease;
}

.talk-button:hover {
  transform: translateY(-2px);

  border-color: #9299a6;

  background: rgba(255, 255, 255, 0.72);
}

.talk-arrow {
  font-size: 16px;
  line-height: 1;
}

.menu-toggle {
  position: relative;

  display: none;

  width: 20px;
  height: 18px;

  padding: 0;

  background: transparent;

  cursor: pointer;
}

.menu-toggle span {
  position: absolute;

  left: 1px;

  width: 18px;
  height: 1px;

  background: #7c838e;

  transition:
    transform 0.3s ease,
    opacity 0.3s ease;
}

.menu-toggle span:first-child {
  top: 6px;
}

.menu-toggle span:last-child {
  top: 11px;
}

.menu-open .menu-toggle span:first-child {
  top: 9px;

  transform: rotate(45deg);
}

.menu-open .menu-toggle span:last-child {
  top: 9px;

  transform: rotate(-45deg);
}

/* =========================================================
   05. MOBILE MENU
========================================================= */

.mobile-menu {
  position: fixed;
  z-index: 950;

  inset: 0;

  pointer-events: auto;
}

.mobile-menu-backdrop {
  position: absolute;

  inset: 0;

  background: rgba(18, 23, 34, 0.16);

  backdrop-filter: blur(10px);
  -webkit-backdrop-filter: blur(10px);
}

.mobile-menu-panel {
  position: absolute;

  top: 0;
  right: 0;
  bottom: 0;

  width: min(430px, 91vw);

  padding: 100px 32px 30px;

  overflow-y: auto;

  background:
    radial-gradient(
      circle at 76% 13%,
      rgba(181, 181, 255, 0.22),
      transparent 29%
    ),
    rgba(247, 247, 249, 0.98);

  border-left: 1px solid rgba(39, 47, 62, 0.08);

  box-shadow: -25px 0 70px rgba(35, 42, 58, 0.11);
}

.lang-fa .mobile-menu-panel {
  right: auto;
  left: 0;

  border-left: 0;

  border-right: 1px solid rgba(39, 47, 62, 0.08);

  box-shadow: 25px 0 70px rgba(35, 42, 58, 0.11);
}

.mobile-menu-top {
  display: flex;
  align-items: center;
  justify-content: space-between;

  color: #8d94a1;

  letter-spacing: 0.18em;

  font-size: 10px;
}

.mobile-menu-top button {
  display: grid;

  width: 36px;
  height: 36px;

  padding: 0;

  place-items: center;

  border: 1px solid rgba(39, 47, 62, 0.12);

  border-radius: 50%;

  color: #1d2430;

  background: rgba(255, 255, 255, 0.5);

  cursor: pointer;

  font-size: 20px;

  transition:
    transform 0.28s ease,
    background 0.28s ease;
}

.mobile-menu-top button:hover {
  transform: rotate(90deg);

  background: #fff;
}

.mobile-menu-panel nav {
  display: flex;
  flex-direction: column;

  margin-top: 36px;
}

.mobile-menu-panel nav a {
  position: relative;

  display: grid;

  grid-template-columns:
    34px
    minmax(0, 1fr)
    auto;

  align-items: center;

  gap: 8px;

  padding: 21px 0;

  border-bottom: 1px solid var(--line);

  color: #1e2531;

  font-size: 24px;

  transition:
    padding 0.32s ease,
    color 0.32s ease;
}

.mobile-menu-panel nav a::before {
  position: absolute;
  content: "";

  left: -10px;
  top: 50%;

  width: 3px;
  height: 0;

  border-radius: 99px;

  background: var(--accent);

  transform: translateY(-50%);

  transition: height 0.3s ease;
}

.mobile-menu-panel nav a:hover {
  padding-left: 10px;
  color: var(--accent);
}

.mobile-menu-panel nav a:hover::before {
  height: 30px;
}

.menu-number {
  color: #a0a6b0;
  font-size: 10px;
}

.menu-arrow {
  color: #858c98;
  font-size: 18px;

  transition: transform 0.28s ease;
}

.mobile-menu-panel nav a:hover .menu-arrow {
  transform: translate(4px, -4px);
}

.lang-fa .mobile-menu-panel nav a {
  grid-template-columns:
    auto
    minmax(0, 1fr)
    34px;

  direction: rtl;
  text-align: right;
}

.lang-fa .mobile-menu-panel nav a::before {
  left: auto;
  right: -10px;
}

.lang-fa .mobile-menu-panel nav a:hover {
  padding-left: 0;
  padding-right: 10px;
}

.lang-fa .mobile-menu-panel nav a:hover .menu-arrow {
  transform: translate(-4px, -4px);
}

.lang-fa .menu-number {
  order: 3;
}

.lang-fa .menu-arrow {
  order: 1;
}

.mobile-menu-bottom {
  display: flex;
  align-items: center;
  justify-content: space-between;

  gap: 20px;

  margin-top: 34px;
  padding-top: 6px;
}

.mobile-menu-bottom button,
.mobile-menu-bottom a {
  color: #343b47;
  font-size: 12px;
}

.mobile-menu-bottom button {
  padding: 0;

  color: #767e8b;

  background: transparent;

  cursor: pointer;
}

.mobile-menu-bottom a {
  display: inline-flex;
  align-items: center;

  gap: 12px;
}

.mobile-menu-bottom a span {
  font-size: 16px;
}

/* =========================================================
   MOBILE MENU TRANSITIONS
========================================================= */

.mobile-menu-enter-active,
.mobile-menu-leave-active {
  transition: opacity 0.42s ease;
}

.mobile-menu-enter-active .mobile-menu-panel,
.mobile-menu-leave-active .mobile-menu-panel {
  transition: transform 0.55s cubic-bezier(0.22, 1, 0.36, 1);
}

.mobile-menu-enter-from,
.mobile-menu-leave-to {
  opacity: 0;
}

.mobile-menu-enter-from .mobile-menu-panel,
.mobile-menu-leave-to .mobile-menu-panel {
  transform: translateX(105%);
}

.lang-fa .mobile-menu-enter-from .mobile-menu-panel,
.lang-fa .mobile-menu-leave-to .mobile-menu-panel {
  transform: translateX(-105%);
}

.mobile-menu-enter-active .mobile-menu-panel nav a {
  opacity: 0;

  transform: translateX(24px);

  transition:
    opacity 0.55s cubic-bezier(0.22, 1, 0.36, 1),
    transform 0.55s cubic-bezier(0.22, 1, 0.36, 1);
}

.lang-fa .mobile-menu-enter-active .mobile-menu-panel nav a {
  transform: translateX(-24px);
}

.mobile-menu-enter-to .mobile-menu-panel nav a {
  opacity: 1;

  transform: translateX(0);
}

.mobile-menu-enter-active .mobile-menu-panel nav a:nth-child(1) {
  transition-delay: 0.1s;
}

.mobile-menu-enter-active .mobile-menu-panel nav a:nth-child(2) {
  transition-delay: 0.15s;
}

.mobile-menu-enter-active .mobile-menu-panel nav a:nth-child(3) {
  transition-delay: 0.2s;
}

.mobile-menu-enter-active .mobile-menu-panel nav a:nth-child(4) {
  transition-delay: 0.25s;
}

.mobile-menu-enter-active .mobile-menu-panel nav a:nth-child(5) {
  transition-delay: 0.3s;
}

.mobile-menu-enter-active .mobile-menu-panel nav a:nth-child(6) {
  transition-delay: 0.35s;
}

.mobile-menu-enter-active .mobile-menu-panel nav a:nth-child(7) {
  transition-delay: 0.4s;
}

/* =========================================================
   06. HERO
========================================================= */

.hero {
  min-height: 780px;
  padding: 158px 0 30px;
}

.hero-container {
  position: relative;
  min-height: 635px;
}

.hero-noise {
  position: absolute;
  inset: 0;

  opacity: 0.02;

  pointer-events: none;

  background-image: url("data:image/svg+xml,%3Csvg viewBox='0 0 180 180' xmlns='http://www.w3.org/2000/svg'%3E%3Cfilter id='n'%3E%3CfeTurbulence type='fractalNoise' baseFrequency='.85' numOctaves='4' stitchTiles='stitch'/%3E%3C/filter%3E%3Crect width='100%25' height='100%25' filter='url(%23n)' opacity='.48'/%3E%3C/svg%3E");
}

.hero-ambient {
  position: absolute;
  border-radius: 50%;

  filter: blur(45px);

  pointer-events: none;
}

.hero-ambient-1 {
  top: 135px;
  left: 45%;

  width: 380px;
  height: 230px;

  background: rgba(207, 207, 255, 0.32);
}

.hero-ambient-2 {
  right: 7%;
  bottom: 65px;

  width: 240px;
  height: 100px;

  background: rgba(196, 223, 255, 0.26);
}

.scroll-rail {
  position: absolute;
  z-index: 8;

  top: 130px;
  left: -26px;

  display: flex;
  flex-direction: column;
  align-items: center;

  gap: 11px;
}

.lang-fa .scroll-rail {
  left: auto;
  right: -26px;
}

.scroll-rail-line {
  position: relative;

  width: 1px;
  height: 160px;

  background: #ccd0d7;
}

.scroll-rail-dot {
  position: absolute;

  left: 50%;
  bottom: -2px;

  width: 5px;
  height: 5px;

  transform: translateX(-50%);

  border-radius: 50%;

  background: #202734;
}

.scroll-rail-text {
  color: #b1b6c0;

  writing-mode: vertical-rl;

  font-size: 9px;
  letter-spacing: 0.08em;
}

.hero-copy {
  position: relative;
  z-index: 20;

  width: 510px;
  max-width: 100%;
}

.eyebrow,
.section-caption {
  display: flex;
  align-items: center;

  gap: 22px;

  color: #222a37;

  letter-spacing: 0.2em;

  font-weight: 600;
}

.eyebrow i,
.section-caption i {
  width: 53px;
  height: 1px;
  flex: 0 0 auto;

  background: #aeb3bc;
}

.hero-title {
  position: relative;

  max-width: 520px;

  margin: 33px 0 28px;

  font-family: "DM Serif Display", serif;

  font-size: clamp(70px, 6.2vw, 93px);

  font-weight: 400;

  letter-spacing: -0.058em;

  line-height: 0.91;
}

.hero-title span {
  display: block;
}

.hero-title-accent {
  color: var(--accent);
  font-style: italic;
}

.hero-title strong {
  display: block;
  font-weight: 400;
}

.hero-description {
  width: 365px;
  max-width: 100%;

  margin: 0;

  color: #9299a8;

  font-size: 14px;

  line-height: 1.8;
}

.hero-actions {
  display: flex;
  align-items: center;

  flex-wrap: wrap;

  gap: 17px;

  margin-top: 30px;
}

.hero-round-button {
  display: grid;

  width: 50px;
  height: 50px;

  place-items: center;

  border-radius: 50%;

  color: #fff;

  background: radial-gradient(circle at 35% 28%, #ddd8ff, #afa7f8 70%);

  box-shadow: 0 14px 32px rgba(130, 117, 241, 0.2);

  transition:
    transform 0.35s ease,
    box-shadow 0.35s ease;
}

.hero-round-button:hover {
  transform: translateY(-3px) rotate(-8deg);

  box-shadow: 0 19px 38px rgba(130, 117, 241, 0.28);
}

.hero-round-button span {
  font-size: 19px;
  direction: ltr;
}

.hero-link {
  font-size: 11px;
  font-weight: 500;
}

.hero-divider {
  width: 40px;
  height: 1px;

  margin-left: 6px;

  background: #c1c5cc;
}

.hero-slide-number {
  color: #9097a4;

  font-size: 10px;
  direction: ltr;
}

/* =========================================================
   07. HERO ART
========================================================= */

.hero-art {
  position: absolute;
  z-index: 5;

  top: -54px;
  right: -28px;

  width: 850px;
  height: 690px;

  perspective: 1400px;

  transform: translate3d(0, 0, 0);

  will-change: transform;

  animation: heroArtFloat 8s ease-in-out infinite;
}

.lang-fa .hero-art {
  right: auto;
  left: -28px;
}

.hero-art > * {
  position: absolute;
}

.art-shadow {
  left: 29%;
  top: 49%;

  width: 450px;
  height: 210px;

  border-radius: 50%;

  background: radial-gradient(
    ellipse,
    rgba(146, 157, 234, 0.35),
    rgba(146, 157, 234, 0) 70%
  );

  filter: blur(21px);

  transform: rotate(-10deg);
}

.glass-petal {
  border: 1px solid rgba(142, 159, 242, 0.46);

  background: linear-gradient(
    145deg,
    rgba(255, 255, 255, 0.86),
    rgba(179, 199, 255, 0.42) 47%,
    rgba(226, 207, 255, 0.24)
  );

  box-shadow:
    inset 0 1px rgba(255, 255, 255, 0.92),
    inset 0 -20px 50px rgba(125, 130, 229, 0.05),
    0 25px 80px rgba(116, 134, 225, 0.08);

  backdrop-filter: blur(8px);
  -webkit-backdrop-filter: blur(8px);
}

.petal-a {
  left: 34%;
  top: 92px;

  width: 255px;
  height: 155px;

  border-radius: 30px 25px 78px 30px;

  transform: rotate(-17deg) skewX(-12deg);

  animation: petalFloatA 8s ease-in-out infinite;
}

.petal-b {
  left: 21%;
  top: 177px;

  width: 175px;
  height: 146px;

  border-radius: 45px 25px 60px 52px;

  transform: rotate(-42deg);

  animation: petalFloatB 9s ease-in-out infinite;
}

.petal-c {
  right: 10%;
  top: 166px;

  width: 175px;
  height: 245px;

  border-radius: 40px 65px 35px 75px;

  transform: rotate(24deg);

  animation: petalFloatC 10s ease-in-out infinite;
}

.petal-d {
  left: 36%;
  bottom: 77px;

  width: 350px;
  height: 150px;

  border-radius: 35% 55% 70% 30%;

  transform: rotate(16deg);

  animation: petalFloatD 9s ease-in-out infinite;
}

.petal-e {
  right: 31%;
  top: 250px;

  width: 130px;
  height: 185px;

  border-radius: 50%;

  transform: rotate(53deg);

  opacity: 0.6;
}

.glass-ribbon {
  border: 1px solid rgba(111, 132, 226, 0.46);

  background: linear-gradient(
    150deg,
    rgba(255, 255, 255, 0.44),
    rgba(160, 179, 255, 0.3),
    rgba(255, 219, 251, 0.18)
  );

  box-shadow:
    inset 0 1px rgba(255, 255, 255, 0.84),
    inset 0 0 30px rgba(134, 144, 240, 0.1);

  backdrop-filter: blur(3px);
}

.ribbon-a {
  left: 25%;
  top: 255px;

  width: 505px;
  height: 225px;

  border-radius: 50%;

  transform: rotate(14deg);

  clip-path: polygon(0 20%, 13% 9%, 97% 45%, 94% 65%, 25% 89%, 4% 74%);

  animation: ribbonFloatA 9s ease-in-out infinite;
}

.ribbon-b {
  left: 18%;
  top: 278px;

  width: 590px;
  height: 235px;

  border-radius: 50%;

  transform: rotate(-6deg);

  opacity: 0.42;

  animation: ribbonFloatB 11s ease-in-out infinite;
}

.main-glass-sphere {
  left: 43%;
  top: 278px;

  width: 156px;
  height: 156px;

  border-radius: 50%;

  background: radial-gradient(
    circle at 30% 24%,
    #fff 0 6%,
    #eceaff 17%,
    #bdb8f8 45%,
    #9ea9ef 68%,
    #b8d7ff 87%,
    rgba(255, 255, 255, 0.3) 100%
  );

  box-shadow:
    inset 13px 10px 24px rgba(255, 255, 255, 0.78),
    inset -13px -15px 28px rgba(87, 93, 187, 0.22),
    0 18px 45px rgba(105, 117, 209, 0.21);

  animation: sphereFloat 6.5s ease-in-out infinite;
}

.sphere-highlight {
  position: absolute;

  inset: 18px 37px 78px 29px;

  border-radius: 50%;

  background: rgba(255, 255, 255, 0.48);

  filter: blur(5px);
}

.art-ring {
  border: 1px solid rgba(52, 69, 136, 0.8);

  border-radius: 50%;
}

.ring-1 {
  left: 17%;
  top: 240px;

  width: 600px;
  height: 220px;

  transform: rotate(14deg);

  animation: ringFloatOne 10s ease-in-out infinite;
}

.ring-2 {
  left: 30%;
  top: 220px;

  width: 460px;
  height: 170px;

  border-color: rgba(113, 127, 203, 0.3);

  transform: rotate(-17deg);

  animation: ringFloatTwo 12s ease-in-out infinite;
}

.ring-3 {
  left: 28%;
  top: 268px;

  width: 390px;
  height: 160px;

  border-color: rgba(255, 255, 255, 0.9);

  transform: rotate(56deg);
}

.mini-sphere {
  border-radius: 50%;

  background: radial-gradient(
    circle at 28% 23%,
    #fff,
    #d8d9ff 35%,
    #96a4e4 72%,
    #6d82d6
  );

  box-shadow:
    inset 4px 4px 10px rgba(255, 255, 255, 0.8),
    0 11px 30px rgba(81, 96, 184, 0.22);
}

.sphere-1 {
  top: 160px;
  right: 14%;

  width: 30px;
  height: 30px;

  animation: miniSphereOne 5s ease-in-out infinite;
}

.sphere-2 {
  left: 15%;
  bottom: 174px;

  width: 42px;
  height: 42px;

  animation: miniSphereTwo 7s ease-in-out infinite;
}

.sphere-3 {
  right: 18%;
  bottom: 255px;

  width: 20px;
  height: 20px;

  animation: miniSphereThree 6s ease-in-out 1s infinite;
}

.sphere-4 {
  left: 39%;
  bottom: 102px;

  width: 19px;
  height: 19px;

  opacity: 0.9;

  animation: miniSphereFour 8s ease-in-out 0.5s infinite;
}

.light-streak {
  left: 33%;
  bottom: 70px;

  width: 390px;
  height: 90px;

  border-radius: 50%;

  background: radial-gradient(
    ellipse,
    rgba(197, 208, 255, 0.44),
    rgba(197, 208, 255, 0) 70%
  );

  filter: blur(10px);

  animation: lightStreakFloat 7s ease-in-out infinite;
}

/* =========================================================
   08. HERO CARDS
========================================================= */

.hero-cards {
  display: contents;
}

.hero-card,
.hero-stats {
  position: absolute;

  z-index: 40;

  min-width: 0;

  border: 1px solid rgba(255, 255, 255, 0.78);

  background: rgba(255, 255, 255, 0.5);

  box-shadow: 0 18px 55px rgba(61, 71, 105, 0.08);

  backdrop-filter: blur(20px);
  -webkit-backdrop-filter: blur(20px);
}

.product-card {
  top: 54px;
  right: 0;

  width: 240px;
  max-width: 100%;

  padding: 18px 19px;

  border-radius: 15px;

  overflow: hidden;

  transition:
    transform 0.45s cubic-bezier(0.22, 1, 0.36, 1),
    box-shadow 0.45s ease;
}

.product-card:hover {
  transform: translateY(-5px);

  box-shadow: 0 25px 60px rgba(61, 71, 105, 0.12);
}

.hero-card-title {
  display: flex;
  align-items: flex-start;

  gap: 9px;

  min-width: 0;

  color: #27303d;

  font-size: 14px;

  line-height: 1.45;
}

.hero-card-title > span:last-child {
  min-width: 0;

  overflow-wrap: anywhere;

  word-break: normal;
}

.status-dot {
  width: 8px;
  height: 8px;

  flex: 0 0 8px;

  margin-top: 4px;

  border-radius: 50%;

  background: #8278f2;

  box-shadow: 0 0 14px rgba(130, 120, 242, 0.45);
}

.product-card p {
  width: 100%;
  max-width: 100%;

  margin: 14px 0 24px;

  color: #737b8b;

  font-size: 12px;

  line-height: 1.7;

  overflow-wrap: anywhere;
}

.hero-card-footer {
  display: flex;
  align-items: center;
  justify-content: space-between;

  color: #9298a4;
}

.hero-card-footer i {
  width: 39px;
  height: 1px;

  background: #c0c4cb;

  transition: width 0.35s ease;
}

.product-card:hover .hero-card-footer i {
  width: 54px;
}

.hero-stats {
  right: 0;
  bottom: 54px;

  width: 175px;

  padding: 13px 18px;

  border-left: 1px solid var(--accent);

  border-radius: 0 14px 14px 0;
}

.stat-item + .stat-item {
  margin-top: 18px;
}

.stat-item strong {
  display: block;

  color: #202734;

  font-size: 17px;

  font-weight: 500;
}

.stat-item span {
  display: block;

  margin-top: 4px;

  color: #9299a7;

  font-size: 10px;

  letter-spacing: 0.04em;
}

/* =========================================================
   09. GENERIC HEADINGS
========================================================= */

.display-title {
  margin: 0;

  font-family: "DM Serif Display", serif;

  font-size: clamp(52px, 5.15vw, 76px);

  font-weight: 400;

  letter-spacing: -0.055em;

  line-height: 0.94;
}

.display-title em {
  color: var(--accent);

  font-style: italic;
}

/* =========================================================
   10. ABOUT
========================================================= */

.about {
  padding: 155px 0;
}

.content-grid,
.expertise-grid {
  display: grid;

  grid-template-columns:
    0.65fr
    1.35fr;

  gap: 55px;
}

.about-content {
  max-width: 760px;
}

.about-content p {
  max-width: 620px;

  margin: 34px 0 0;

  color: #878f9e;

  font-size: 14px;

  line-height: 1.8;
}

.about-stats {
  display: grid;

  grid-template-columns: repeat(3, minmax(0, 1fr));

  gap: 20px;

  margin-top: 45px;
  padding-top: 23px;

  border-top: 1px solid var(--line);
}

.about-stat strong {
  display: block;

  color: #202734;

  font-size: 29px;

  font-weight: 500;
}

.about-stat span {
  display: block;

  margin-top: 6px;

  color: #8e96a4;

  font-size: 9px;

  letter-spacing: 0.04em;
}

/* =========================================================
   11. SERVICES
========================================================= */

.services {
  padding: 25px 0 130px;
}

.section-head {
  margin-bottom: 24px;
}

.services-grid {
  display: grid;

  grid-template-columns: repeat(3, 1fr);
}

.service-item {
  min-height: 150px;

  padding: 18px 24px 18px 17px;

  border-bottom: 1px solid var(--line);

  border-right: 1px solid var(--line);
}

.service-item:nth-child(3n) {
  border-right: 0;
}

.service-number {
  color: #9299a7;

  font-size: 10px;
}

.service-body {
  margin-top: 13px;

  min-width: 0;
}

.service-body h2 {
  margin: 0;

  max-width: 250px;

  color: #222a37;

  font-size: 14px;

  font-weight: 500;

  line-height: 1.4;
}

.service-body p {
  max-width: 235px;

  margin: 9px 0 0;

  color: #8b93a1;

  font-size: 10px;

  line-height: 1.75;
}

.services-work-link {
  display: flex;

  align-items: center;
  justify-content: center;

  min-height: 150px;

  gap: 14px;

  color: #5d6573;

  font-size: 10px;
}

.services-work-link strong {
  color: #47505e;

  font-size: 16px;

  font-weight: 400;

  direction: ltr;
}

.services-orb {
  display: grid;

  width: 64px;
  height: 64px;

  place-items: center;

  border-radius: 50%;

  flex: 0 0 auto;

  background: radial-gradient(circle at 30% 25%, #e5e4ff, #b6b0fa 52%, #f3f2ff);

  box-shadow:
    inset 0 0 0 9px rgba(255, 255, 255, 0.4),
    0 15px 34px rgba(121, 110, 231, 0.12);

  transition: transform 0.45s cubic-bezier(0.22, 1, 0.36, 1);
}

.services-orb span {
  font-size: 17px;
}

.services-work-link:hover .services-orb {
  transform: rotate(12deg) scale(1.06);
}

/* =========================================================
   12. EXPERTISE
========================================================= */

.expertise {
  padding: 140px 0;

  background: var(--page-bg-2);
}

.expertise-content {
  max-width: 760px;
}

.expertise-content p {
  max-width: 560px;

  margin: 35px 0 0;

  color: #838b99;

  font-size: 14px;

  line-height: 1.8;
}

.expertise-tags {
  display: flex;

  flex-wrap: wrap;

  gap: 9px;

  margin-top: 35px;
}

.expertise-tags span {
  padding: 10px 14px;

  border: 1px solid rgba(56, 63, 77, 0.14);

  border-radius: 999px;

  color: #757d8c;

  background: rgba(255, 255, 255, 0.3);

  font-size: 10px;

  transition:
    transform 0.3s ease,
    background 0.3s ease,
    color 0.3s ease;
}

.expertise-tags span.active {
  color: #3b365f;

  border-color: rgba(132, 121, 244, 0.28);

  background: rgba(132, 121, 244, 0.12);
}

.expertise-tags span:hover {
  transform: translateY(-2px);
}

/* =========================================================
   13. TESTIMONIALS
========================================================= */

.testimonials {
  padding: 145px 0 130px;
}

.testimonials-grid {
  display: grid;

  grid-template-columns: repeat(2, minmax(0, 1fr));

  gap: 24px;

  margin-top: 52px;
}

.testimonial-card {
  min-width: 0;
}

.testimonial-card__box {
  position: relative;

  min-height: 240px;

  padding: 31px;

  border-radius: 20px;

  border: 1px solid rgba(255, 255, 255, 0.8);

  background: rgba(255, 255, 255, 0.48);

  box-shadow: 0 18px 55px rgba(61, 71, 105, 0.06);

  backdrop-filter: blur(18px);
  -webkit-backdrop-filter: blur(18px);
}

.testimonial-quote {
  position: absolute;

  top: 180px;

  color: var(--accent);

  font-family: "DM Serif Display", serif;

  font-size: 60px;

  line-height: 1;

  opacity: 0.35;

  inset-inline-end: 24px;
}

.testimonial-card__box p {
  margin: 0;

  padding-right: 20px;

  color: #727b89;

  font-size: 13px;

  line-height: 2;
}

.testimonial-stars {
  display: flex;

  gap: 3px;

  margin-top: 24px;

  color: var(--accent);

  font-size: 12px;

  direction: ltr;
}

.testimonial-client {
  display: flex;

  align-items: center;

  gap: 13px;

  margin-top: 16px;

  padding-left: 5px;

  min-width: 0;
}

.testimonial-client img {
  width: 38px;
  height: 38px;

  flex: 0 0 38px;

  border-radius: 50%;

  object-fit: cover;

  filter: saturate(0.85);
}

.testimonial-client div {
  min-width: 0;
}

.testimonial-client strong {
  display: block;

  color: #202734;

  font-size: 11px;

  font-weight: 600;
}

.testimonial-client span {
  display: block;

  margin-top: 4px;

  color: #8e96a3;

  font-size: 9px;

  line-height: 1.4;
}

/* =========================================================
   14. WORK
========================================================= */

.work {
  padding: 130px 0 145px;

  background: var(--page-bg-2);
}

.work-top {
  display: grid;

  grid-template-columns:
    0.65fr
    1.35fr;

  gap: 55px;

  margin-bottom: 64px;
}

.work-grid {
  display: grid;

  grid-template-columns: repeat(2, minmax(0, 1fr));

  gap: 58px 24px;
}

.project {
  min-width: 0;
}

.project-large {
  grid-column: span 2;
}

.project-visual {
  position: relative;

  overflow: hidden;

  min-height: 370px;

  border-radius: 22px;

  background: radial-gradient(
    circle at 50% 45%,
    hsla(var(--hue), 100%, 94%, 0.96),
    rgba(220, 224, 245, 0.9) 32%,
    rgba(230, 231, 237, 1) 70%,
    rgba(245, 245, 247, 1)
  );

  isolation: isolate;
}

.project-large .project-visual {
  min-height: 520px;
}

.project-photo::before {
  position: absolute;

  content: "";

  inset: 0;

  background:
    linear-gradient(
      135deg,
      rgba(255, 255, 255, 0.82),
      rgba(255, 255, 255, 0.08)
    ),
    var(--project-image) center / cover no-repeat;

  opacity: 0.78;

  transform: scale(1.03);

  transition:
    transform 0.7s cubic-bezier(0.22, 1, 0.36, 1),
    opacity 0.7s ease;
}

.project:hover .project-photo::before {
  transform: scale(1.08);
  opacity: 0.9;
}

.project-overlay {
  position: absolute;

  inset: 0;

  z-index: 1;

  background: linear-gradient(
    180deg,
    rgba(237, 239, 250, 0.12),
    rgba(112, 119, 173, 0.3)
  );

  pointer-events: none;
}

.project-glow {
  position: absolute;

  left: 50%;
  top: 50%;

  width: 330px;
  height: 210px;

  z-index: 2;

  transform: translate(-50%, -50%);

  border-radius: 50%;

  background: radial-gradient(
    ellipse,
    hsla(var(--hue), 95%, 78%, 0.36),
    hsla(var(--hue), 95%, 78%, 0) 72%
  );

  filter: blur(22px);
}

/* =========================================================
   PROJECT SHAPES — HOVER ONLY
========================================================= */

.project-shape {
  position: absolute;
  z-index: 3;

  border: 1px solid hsla(var(--hue), 50%, 58%, 0.4);

  background: linear-gradient(
    140deg,
    rgba(255, 255, 255, 0.62),
    hsla(var(--hue), 80%, 85%, 0.24),
    rgba(255, 222, 252, 0.14)
  );

  box-shadow: inset 0 1px rgba(255, 255, 255, 0.9);

  backdrop-filter: blur(5px);
  -webkit-backdrop-filter: blur(5px);

  opacity: 0;
  visibility: hidden;

  pointer-events: none;

  transition:
    opacity 0.5s ease,
    visibility 0.5s ease,
    transform 0.7s cubic-bezier(0.22, 1, 0.36, 1),
    filter 0.6s ease;
}

.shape-one {
  left: 35%;
  top: 30%;

  width: 270px;
  height: 180px;

  border-radius: 40px 65px 35px 80px;

  transform: rotate(-22deg) scale(0.72);

  filter: blur(10px);
}

.shape-two {
  right: 19%;
  top: 26%;

  width: 160px;
  height: 220px;

  border-radius: 55px 35px 70px 35px;

  transform: rotate(30deg) scale(0.72);

  filter: blur(10px);
}

/* فقط هنگام هاور پروژه نمایش داده شوند */
.project:hover .project-shape {
  opacity: 1;
  visibility: visible;

  filter: blur(0);
}

.project:hover .shape-one {
  transform: rotate(-22deg) scale(1);
}

.project:hover .shape-two {
  transform: rotate(30deg) scale(1);
}

.shape-one {
  left: 35%;
  top: 30%;

  width: 270px;
  height: 180px;

  border-radius: 40px 65px 35px 80px;

  transform: rotate(-22deg);
}

.shape-two {
  right: 19%;
  top: 26%;

  width: 160px;
  height: 220px;

  border-radius: 55px 35px 70px 35px;

  transform: rotate(30deg);
}

.project-sphere {
  position: absolute;

  left: 50%;
  top: 50%;

  z-index: 4;

  width: 165px;

  aspect-ratio: 1;

  transform: translate(-50%, -50%);

  border-radius: 50%;

  background: radial-gradient(
    circle at 30% 24%,
    #fff,
    hsla(var(--hue), 65%, 93%, 1) 24%,
    hsla(var(--hue), 58%, 74%, 1) 58%,
    hsla(var(--hue), 50%, 58%, 1) 83%
  );

  box-shadow:
    inset 11px 8px 20px rgba(255, 255, 255, 0.75),
    0 25px 48px hsla(var(--hue), 55%, 50%, 0.16);

  transition: transform 0.65s cubic-bezier(0.22, 1, 0.36, 1);
}

.project:hover .project-sphere {
  transform: translate(-50%, -50%) scale(1.07) rotate(8deg);
}

.project-orbit {
  position: absolute;

  left: 50%;
  top: 50%;

  z-index: 3;

  width: 390px;
  height: 150px;

  transform: translate(-50%, -50%) rotate(17deg);

  border: 1px solid hsla(var(--hue), 45%, 55%, 0.28);

  border-radius: 50%;
}

.orbit-b {
  width: 320px;

  transform: translate(-50%, -50%) rotate(-27deg);
}

.project-meta {
  display: flex;

  align-items: flex-start;

  justify-content: space-between;

  gap: 20px;

  padding: 17px 3px 0;
}

.project-meta > div {
  min-width: 0;
}

.project-meta > div span {
  color: #9198a5;

  font-size: 19px;
}

.project-meta h3 {
  margin: 6px 0 0;

  color: #1f2631;

  font-size: 18px;

  font-weight: 500;

  line-height: 1.5;
}

.project-arrow {
  color: #6d7482;

  font-size: 18px;

  flex: 0 0 auto;

  direction: ltr;
}

/* =========================================================
   15. CTA
========================================================= */

.cta {
  padding: 110px 0 145px;
}

.cta-panel {
  display: grid;

  grid-template-columns:
    1.2fr
    auto;

  align-items: end;

  gap: 50px;

  min-height: 385px;

  padding: 64px;

  border-radius: 25px;

  background:
    radial-gradient(
      circle at 76% 40%,
      rgba(171, 163, 255, 0.28),
      transparent 34%
    ),
    linear-gradient(135deg, #eeeef4, #e6e6ed);
}

.cta-panel p {
  max-width: 500px;

  margin: 30px 0 0;

  color: #838b9a;

  font-size: 14px;

  line-height: 1.8;
}

.pill-link {
  display: inline-flex;

  align-items: center;
  justify-content: center;

  gap: 15px;

  padding: 14px 18px;

  border: 1px solid #aeb3bd;

  border-radius: 999px;

  color: #1f2631;

  font-size: 11px;

  white-space: nowrap;

  transition:
    transform 0.3s ease,
    background 0.3s ease;
}

.pill-link:hover {
  transform: translateY(-2px);

  background: rgba(255, 255, 255, 0.55);
}

.pill-link strong {
  font-size: 16px;

  font-weight: 400;

  direction: ltr;
}

/* =========================================================
   16. CONTACT
========================================================= */

.contact {
  padding: 120px 0 155px;
}

.contact-wrapper {
  display: grid;

  grid-template-columns:
    1.05fr
    0.95fr;

  gap: 70px;

  align-items: center;
}

.office-content > .display-title {
  margin-top: 45px;
}

.contact-cards {
  display: grid;

  grid-template-columns: repeat(2, minmax(0, 1fr));

  gap: 18px;

  margin-top: 50px;
}

.contact-card {
  min-width: 0;

  padding: 24px;

  border: 1px solid rgba(255, 255, 255, 0.74);

  border-radius: 19px;

  background: rgba(255, 255, 255, 0.46);

  box-shadow: 0 15px 45px rgba(61, 71, 105, 0.06);

  backdrop-filter: blur(18px);
  -webkit-backdrop-filter: blur(18px);
}

.contact-card-label {
  color: #979eaa;

  font-size: 9px;

  letter-spacing: 0.15em;
}

.contact-card h3 {
  margin: 13px 0 0;

  color: #222a37;

  font-size: 15px;

  font-weight: 600;
}

.contact-card p {
  margin: 12px 0 0;

  color: #858d9b;

  font-size: 11px;

  line-height: 1.8;
}

.contact-details {
  display: flex;

  flex-direction: column;

  gap: 6px;

  margin-top: 18px;
}

.contact-details a {
  color: #6e7684;

  font-size: 10px;

  overflow-wrap: anywhere;
}

.contact-visual {
  position: relative;

  min-height: 510px;

  overflow: hidden;

  border-radius: 30px;

  background: radial-gradient(
    circle at 50% 50%,
    rgba(209, 211, 255, 0.8),
    rgba(228, 229, 239, 0.85) 46%,
    #eff0f4
  );

  isolation: isolate;
}

.contact-visual-glow {
  position: absolute;

  left: 50%;
  top: 50%;

  width: 360px;
  height: 360px;

  transform: translate(-50%, -50%);

  border-radius: 50%;

  background: radial-gradient(
    circle,
    rgba(144, 132, 245, 0.3),
    transparent 67%
  );

  filter: blur(25px);
}

.contact-orbit {
  position: absolute;

  left: 50%;
  top: 50%;

  border: 1px solid rgba(119, 128, 203, 0.34);

  border-radius: 50%;

  transform: translate(-50%, -50%);
}

.orbit-contact-1 {
  width: 430px;
  height: 180px;

  transform: translate(-50%, -50%) rotate(24deg);
}

.orbit-contact-2 {
  width: 330px;
  height: 150px;

  transform: translate(-50%, -50%) rotate(-33deg);
}

.contact-sphere {
  position: absolute;

  left: 50%;
  top: 50%;

  width: 180px;
  height: 180px;

  transform: translate(-50%, -50%);

  border-radius: 50%;

  background: radial-gradient(
    circle at 28% 21%,
    #fff,
    #ddd9ff 28%,
    #afa8ef 62%,
    #8ea9e6 100%
  );

  box-shadow:
    inset 13px 10px 25px rgba(255, 255, 255, 0.84),
    inset -12px -12px 25px rgba(80, 86, 173, 0.18),
    0 35px 70px rgba(112, 102, 214, 0.2);

  animation: sphereFloat 6s ease-in-out infinite;
}

.contact-center {
  position: absolute;

  left: 50%;
  top: 50%;

  display: grid;

  width: 68px;
  height: 68px;

  place-items: center;

  transform: translate(-50%, -50%);

  border-radius: 50%;

  color: #fff;

  background: rgba(125, 116, 220, 0.75);

  box-shadow: 0 14px 35px rgba(87, 78, 183, 0.2);

  backdrop-filter: blur(8px);
}

.contact-center span {
  font-size: 15px;

  font-weight: 700;

  letter-spacing: 0.08em;

  direction: ltr;
}

.contact-mail {
  position: absolute;

  left: 50%;
  bottom: 42px;

  max-width: calc(100% - 40px);

  transform: translateX(-50%);

  padding-bottom: 7px;

  border-bottom: 1px solid rgba(99, 106, 120, 0.45);

  color: #343b47;

  font-size: 10px;

  white-space: nowrap;

  direction: ltr;
}

/* =========================================================
   17. FOOTER
========================================================= */

.footer {
  padding: 65px 0 32px;
}

.footer-top {
  display: grid;

  grid-template-columns:
    minmax(240px, 0.9fr)
    minmax(0, 1.1fr);

  gap: 70px;

  padding-bottom: 58px;

  border-bottom: 1px solid var(--line);
}

.footer-brand-block p {
  max-width: 340px;

  margin: 23px 0 0;

  color: #8b93a0;

  font-size: 11px;

  line-height: 1.8;
}

.footer-brand-block small {
  display: block;

  margin-top: 22px;

  color: #9aa0ab;

  font-size: 9px;
}

.footer-columns {
  display: grid;

  grid-template-columns: repeat(3, 1fr);

  gap: 25px;
}

.footer-col__toggle {
  display: flex;

  align-items: center;

  justify-content: space-between;

  width: 100%;

  padding: 0;

  color: #232a36;

  background: transparent;

  cursor: pointer;

  font-size: 10px;

  font-weight: 600;

  letter-spacing: 0.12em;

  text-transform: uppercase;
}

.footer-col__arrow {
  display: none;
}

.footer-col__links {
  display: flex;

  flex-direction: column;

  gap: 12px;

  margin-top: 19px;
}

.footer-col__links a {
  color: #8b93a1;

  font-size: 10px;

  line-height: 1.5;

  transition: color 0.25s ease;
}

.footer-col__links a:hover {
  color: #363e4d;
}

.footer-bottom {
  display: flex;

  align-items: center;

  justify-content: space-between;

  gap: 24px;

  padding-top: 21px;

  color: #949ba7;

  font-size: 9px;
}

.footer-social {
  display: flex;

  align-items: center;

  gap: 22px;

  min-width: 0;
}

.socials {
  display: flex;

  align-items: center;

  gap: 8px;
}

.socials a {
  display: grid;

  width: 29px;
  height: 29px;

  place-items: center;

  border: 1px solid rgba(83, 90, 104, 0.14);

  border-radius: 50%;

  color: #7b8390;

  font-size: 8px;

  direction: ltr;

  transition:
    transform 0.3s ease,
    color 0.3s ease,
    border-color 0.3s ease;
}

.socials a:hover {
  transform: translateY(-2px);

  color: #333b48;

  border-color: rgba(83, 90, 104, 0.3);
}

.footer-social select {
  min-width: 115px;
  max-width: 145px;

  padding: 8px 10px;

  border: 1px solid rgba(83, 90, 104, 0.14);

  border-radius: 999px;

  color: #747d8b;

  background: rgba(255, 255, 255, 0.4);

  outline: 0;

  font-size: 9px;

  cursor: pointer;
}

/* =========================================================
   18. TO TOP
========================================================= */

.to-top {
  position: fixed;

  z-index: 800;

  right: 25px;
  bottom: 25px;

  display: grid;

  width: 43px;
  height: 43px;

  place-items: center;

  border-radius: 50%;

  color: #fff;

  background: linear-gradient(135deg, #a59df8, #8277eb);

  box-shadow: 0 14px 32px rgba(108, 98, 201, 0.25);

  cursor: pointer;

  opacity: 0;
  visibility: hidden;

  transform: translateY(15px) scale(0.9);

  transition:
    opacity 0.3s ease,
    visibility 0.3s ease,
    transform 0.3s ease;
}

.to-top.show {
  opacity: 1;

  visibility: visible;

  transform: translateY(0) scale(1);
}

.to-top:hover {
  transform: translateY(-3px) scale(1.04);
}

.lang-fa .to-top {
  right: auto;
  left: 25px;
}

/* =========================================================
   19. REVEAL
========================================================= */

.reveal {
  opacity: 0;

  transform: translate3d(0, 34px, 0) scale(0.985);

  filter: blur(4px);

  transition:
    opacity 0.9s cubic-bezier(0.22, 1, 0.36, 1),
    transform 0.9s cubic-bezier(0.22, 1, 0.36, 1),
    filter 0.9s cubic-bezier(0.22, 1, 0.36, 1);
}

.reveal-delay-1 {
  transition-delay: 0.11s;
}

.reveal-delay-2 {
  transition-delay: 0.22s;
}

.reveal.is-visible {
  opacity: 1;

  transform: translate3d(0, 0, 0) scale(1);

  filter: blur(0);
}

/* =========================================================
   20. PAGE ENTRY
========================================================= */

.site-shell:not(.page-ready) main,
.site-shell:not(.page-ready) .site-header,
.site-shell:not(.page-ready) .footer {
  opacity: 0;
}

.site-shell.page-ready main,
.site-shell.page-ready .site-header,
.site-shell.page-ready .footer {
  animation: pageContentIn 1s cubic-bezier(0.22, 1, 0.36, 1) forwards;
}

.site-shell.page-ready .hero-copy {
  animation: heroEntry 1.1s 0.12s cubic-bezier(0.22, 1, 0.36, 1) both;
}

.site-shell.page-ready .hero-art {
  animation: heroArtEntry 1.25s 0.1s cubic-bezier(0.22, 1, 0.36, 1) both;
}

.site-shell.page-ready.lang-fa .hero-art {
  animation: heroArtEntryFa 1.25s 0.1s cubic-bezier(0.22, 1, 0.36, 1) both;
}

.site-shell.page-ready .product-card {
  animation: cardEntry 0.95s 0.48s cubic-bezier(0.22, 1, 0.36, 1) both;
}

.site-shell.page-ready .hero-stats {
  animation: cardEntry 1s 0.62s cubic-bezier(0.22, 1, 0.36, 1) both;
}

.hero-title > * {
  opacity: 0;

  transform: translate3d(0, 28px, 0);
}

.hero-copy.is-visible .hero-title > * {
  animation: heroTextIn 0.85s cubic-bezier(0.22, 1, 0.36, 1) forwards;
}

.hero-copy.is-visible .hero-title > :nth-child(1) {
  animation-delay: 0.08s;
}

.hero-copy.is-visible .hero-title > :nth-child(2) {
  animation-delay: 0.16s;
}

.hero-copy.is-visible .hero-title > :nth-child(3) {
  animation-delay: 0.24s;
}

.hero-copy.is-visible .hero-title > :nth-child(4) {
  animation-delay: 0.32s;
}

.service-item,
.project,
.testimonial-card,
.contact-card,
.expertise-tags span {
  will-change: transform;
}

.service-item {
  transition:
    transform 0.35s ease,
    opacity 0.9s ease,
    filter 0.9s ease;
}

.service-item:hover {
  transform: translateY(-4px);
}

.project,
.testimonial-card,
.contact-card {
  transition: transform 0.35s ease;
}

.project:hover,
.testimonial-card:hover {
  transform: translateY(-4px);
}

@keyframes pageContentIn {
  from {
    opacity: 0;
  }

  to {
    opacity: 1;
  }
}

@keyframes heroEntry {
  from {
    opacity: 0;

    transform: translate3d(0, 34px, 0) scale(0.985);

    filter: blur(8px);
  }

  to {
    opacity: 1;

    transform: translate3d(0, 0, 0) scale(1);

    filter: blur(0);
  }
}

@keyframes heroArtEntry {
  from {
    opacity: 0;

    transform: translate3d(38px, 24px, 0) scale(0.92);

    filter: blur(12px);
  }

  to {
    opacity: 1;

    transform: translate3d(0, 0, 0) scale(1);

    filter: blur(0);
  }
}

@keyframes heroArtEntryFa {
  from {
    opacity: 0;

    transform: translate3d(-38px, 24px, 0) scale(0.92);

    filter: blur(12px);
  }

  to {
    opacity: 1;

    transform: translate3d(0, 0, 0) scale(1);

    filter: blur(0);
  }
}

@keyframes heroArtEntryMobile {
  from {
    opacity: 0;

    transform: translate3d(38px, 24px, 0) scale(var(--art-scale));

    filter: blur(12px);
  }

  to {
    opacity: 1;

    transform: translate3d(0, 0, 0) scale(var(--art-scale));

    filter: blur(0);
  }
}

@keyframes heroArtEntryMobileFa {
  from {
    opacity: 0;

    transform: translate3d(-38px, 24px, 0) scale(var(--art-scale));

    filter: blur(12px);
  }

  to {
    opacity: 1;

    transform: translate3d(0, 0, 0) scale(var(--art-scale));

    filter: blur(0);
  }
}

@keyframes cardEntry {
  from {
    opacity: 0;

    transform: translate3d(0, 28px, 0) scale(0.94);

    filter: blur(7px);
  }

  to {
    opacity: 1;

    transform: translate3d(0, 0, 0) scale(1);

    filter: blur(0);
  }
}

@keyframes heroTextIn {
  to {
    opacity: 1;

    transform: translate3d(0, 0, 0);
  }
}

/* =========================================================
   21. ART ANIMATIONS
========================================================= */

.glass-petal,
.glass-ribbon,
.main-glass-sphere,
.art-ring,
.mini-sphere {
  will-change: transform;
}

@keyframes heroArtFloat {
  0%,
  100% {
    translate: 0 0;
  }

  50% {
    translate: 0 -9px;
  }
}

@keyframes petalFloatA {
  0%,
  100% {
    transform: rotate(-17deg) translate3d(0, 0, 0);
  }

  50% {
    transform: rotate(-13deg) translate3d(0, -13px, 0);
  }
}

@keyframes petalFloatB {
  0%,
  100% {
    transform: rotate(-42deg) translate3d(0, 0, 0);
  }

  50% {
    transform: rotate(-37deg) translate3d(0, -15px, 0);
  }
}

@keyframes petalFloatC {
  0%,
  100% {
    transform: rotate(24deg) translate3d(0, 0, 0);
  }

  50% {
    transform: rotate(20deg) translate3d(0, 16px, 0);
  }
}

@keyframes petalFloatD {
  0%,
  100% {
    transform: rotate(16deg) translate3d(0, 0, 0);
  }

  50% {
    transform: rotate(11deg) translate3d(0, -9px, 0);
  }
}

@keyframes ribbonFloatA {
  0%,
  100% {
    transform: rotate(14deg) translate3d(0, 0, 0);
  }

  50% {
    transform: rotate(16deg) translate3d(0, -8px, 0);
  }
}

@keyframes ribbonFloatB {
  0%,
  100% {
    transform: rotate(-6deg) translate3d(0, 0, 0);
  }

  50% {
    transform: rotate(-4deg) translate3d(0, 9px, 0);
  }
}

@keyframes sphereFloat {
  0%,
  100% {
    transform: translate3d(0, 0, 0) scale(1);
  }

  50% {
    transform: translate3d(0, -15px, 0) scale(1.025);
  }
}

@keyframes ringFloatOne {
  0%,
  100% {
    transform: rotate(14deg) scale(1);
  }

  50% {
    transform: rotate(17deg) scale(1.02);
  }
}

@keyframes ringFloatTwo {
  0%,
  100% {
    transform: rotate(-17deg) scale(1);
  }

  50% {
    transform: rotate(-13deg) scale(1.03);
  }
}

@keyframes miniSphereOne {
  0%,
  100% {
    transform: translate3d(0, 0, 0);
  }

  50% {
    transform: translate3d(-5px, -16px, 0);
  }
}

@keyframes miniSphereTwo {
  0%,
  100% {
    transform: translate3d(0, 0, 0);
  }

  50% {
    transform: translate3d(8px, -14px, 0);
  }
}

@keyframes miniSphereThree {
  0%,
  100% {
    transform: translate3d(0, 0, 0);
  }

  50% {
    transform: translate3d(6px, 11px, 0);
  }
}

@keyframes miniSphereFour {
  0%,
  100% {
    transform: translate3d(0, 0, 0);
  }

  50% {
    transform: translate3d(-5px, -10px, 0);
  }
}

@keyframes lightStreakFloat {
  0%,
  100% {
    opacity: 0.72;

    transform: translate3d(0, 0, 0) scale(1);
  }

  50% {
    opacity: 1;

    transform: translate3d(0, -8px, 0) scale(1.04);
  }
}

/* =========================================================
   22. MINI GLASS TECH OBJECT
========================================================= */

@media (max-width: 900px) {
  .hero-title::before {
    position: absolute;
    content: "";

    top: -2px;
    right: -1%;

    width: 92px;
    height: 92px;

    border: 1px solid rgba(132, 121, 244, 0.28);

    border-radius: 24px;

    background:
      radial-gradient(
        circle at 50% 50%,
        rgba(255, 255, 255, 0.95) 0 5%,
        rgba(214, 208, 255, 0.52) 14%,
        transparent 40%
      ),
      radial-gradient(
        circle at 24% 19%,
        rgba(255, 255, 255, 1) 0 5px,
        rgba(255, 255, 255, 0.55) 6px,
        transparent 13px
      ),
      radial-gradient(
        circle at 76% 75%,
        rgba(132, 121, 244, 0.3),
        transparent 36%
      ),
      linear-gradient(
        135deg,
        rgba(255, 255, 255, 0.96),
        rgba(225, 221, 255, 0.72) 34%,
        rgba(182, 193, 255, 0.42) 68%,
        rgba(139, 168, 245, 0.16)
      );

    box-shadow:
      inset 2px 2px 0 rgba(255, 255, 255, 0.98),
      inset -14px -15px 28px rgba(71, 79, 169, 0.11),
      inset 0 0 22px rgba(255, 255, 255, 0.28),
      0 18px 42px rgba(100, 89, 213, 0.15),
      0 0 55px rgba(132, 121, 244, 0.14);

    backdrop-filter: blur(10px);
    -webkit-backdrop-filter: blur(10px);

    pointer-events: none;

    transform: rotate(18deg);

    animation:
      miniTechFloat 5.2s ease-in-out infinite,
      miniTechGlow 4s ease-in-out infinite;
  }

  .hero-title::before {
    box-shadow:
      inset 2px 2px 0 rgba(255, 255, 255, 0.98),
      inset -14px -15px 28px rgba(71, 79, 169, 0.11),
      inset 0 0 22px rgba(255, 255, 255, 0.28),
      0 18px 42px rgba(100, 89, 213, 0.15),
      0 0 55px rgba(132, 121, 244, 0.14);
  }

  .hero-title::after {
    position: absolute;
    content: "";

    top: -13px;
    right: -15px;

    width: 116px;
    height: 116px;

    border: 1px solid rgba(132, 121, 244, 0.2);

    border-radius: 50%;

    background:
      linear-gradient(
        90deg,
        transparent 47.8%,
        rgba(132, 121, 244, 0.28) 48.5% 51.5%,
        transparent 52.2%
      ),
      linear-gradient(
        0deg,
        transparent 47.8%,
        rgba(132, 121, 244, 0.23) 48.5% 51.5%,
        transparent 52.2%
      ),
      linear-gradient(
        45deg,
        transparent 48.8%,
        rgba(132, 121, 244, 0.13) 49.3% 50.7%,
        transparent 51.2%
      ),
      radial-gradient(
        circle at 50% 50%,
        rgba(132, 121, 244, 0.12) 0 15%,
        transparent 16%
      );

    box-shadow:
      inset 0 0 0 8px rgba(255, 255, 255, 0.06),
      inset 0 0 24px rgba(132, 121, 244, 0.08),
      0 0 35px rgba(132, 121, 244, 0.1);

    pointer-events: none;

    animation:
      miniTechOrbit 9s linear infinite,
      miniTechRingPulse 4.5s ease-in-out infinite;
  }

  .hero-title {
    --tech-dot-size: 7px;
  }

  .hero-title::after {
    outline: 1px solid rgba(132, 121, 244, 0.08);

    outline-offset: 6px;
  }

  .lang-fa .hero-title::before {
    right: auto;
    left: -1%;
  }

  .lang-fa .hero-title::after {
    right: auto;
    left: -15px;
  }
}

@keyframes miniTechFloat {
  0%,
  100% {
    transform: translate3d(0, 0, 0) rotate(18deg) scale(0.96);
  }

  25% {
    transform: translate3d(2px, -5px, 0) rotate(24deg) scale(1);
  }

  50% {
    transform: translate3d(0, -12px, 0) rotate(34deg) scale(1.05);
  }

  75% {
    transform: translate3d(-2px, -5px, 0) rotate(27deg) scale(1);
  }
}

@keyframes miniTechGlow {
  0%,
  100% {
    opacity: 0.78;

    filter: brightness(0.98) saturate(0.92);
  }

  50% {
    opacity: 1;

    filter: brightness(1.09) saturate(1.08);
  }
}

@keyframes miniTechOrbit {
  0% {
    transform: rotate(0deg) scale(0.92);

    opacity: 0.28;
  }

  25% {
    opacity: 0.55;
  }

  50% {
    transform: rotate(180deg) scale(1.06);

    opacity: 0.8;
  }

  75% {
    opacity: 0.45;
  }

  100% {
    transform: rotate(360deg) scale(0.92);

    opacity: 0.28;
  }
}

@keyframes miniTechRingPulse {
  0%,
  100% {
    box-shadow:
      inset 0 0 0 8px rgba(255, 255, 255, 0.06),
      inset 0 0 24px rgba(132, 121, 244, 0.06),
      0 0 28px rgba(132, 121, 244, 0.04);
  }

  50% {
    box-shadow:
      inset 0 0 0 9px rgba(255, 255, 255, 0.1),
      inset 0 0 34px rgba(132, 121, 244, 0.13),
      0 0 48px rgba(132, 121, 244, 0.13);
  }
}

/* =========================================================
   640px
========================================================= */

@media (max-width: 640px) {
  .hero-title::before {
    top: -2px;
    right: -1%;

    width: 72px;
    height: 72px;

    border-radius: 20px;
  }

  .hero-title::after {
    top: -10px;
    right: -11px;

    width: 92px;
    height: 92px;
  }

  .lang-fa .hero-title::before {
    left: -1%;
    right: auto;
  }

  .lang-fa .hero-title::after {
    left: -11px;
    right: auto;
  }
}

/* =========================================================
   420px
========================================================= */

@media (max-width: 420px) {
  .hero-title::before {
    top: -1px;
    right: 0;

    width: 58px;
    height: 58px;

    border-radius: 17px;
  }

  .hero-title::after {
    top: -8px;
    right: -8px;

    width: 74px;
    height: 74px;
  }

  .lang-fa .hero-title::before {
    left: 0;
    right: auto;
  }

  .lang-fa .hero-title::after {
    left: -8px;
    right: auto;
  }
}

/* =========================================================
   23. RTL
========================================================= */

.lang-fa {
  direction: rtl;

  font-family: "Vazirmatn", sans-serif;
}

.lang-fa .brand-name {
  direction: rtl;

  font-family: "Vazirmatn", sans-serif;

  letter-spacing: 0;

  font-size: 18px;

  font-weight: 600;
}

.lang-fa .header-inner {
  direction: rtl;
}

.lang-fa .header-actions {
  direction: rtl;
}

.lang-fa .desktop-nav {
  direction: rtl;
}

.lang-fa .hero-copy,
.lang-fa .hero-description,
.lang-fa .section-caption,
.lang-fa .section-head,
.lang-fa .service-body,
.lang-fa .about-content,
.lang-fa .expertise-content,
.lang-fa .testimonial-card,
.lang-fa .project-meta,
.lang-fa .office-content,
.lang-fa .cta-panel,
.lang-fa .footer-top,
.lang-fa .footer-bottom,
.lang-fa .contact-card {
  direction: rtl;
}

.lang-fa .hero-copy {
  text-align: right;
}

.lang-fa .hero-title,
.lang-fa .display-title {
  font-family: "Vazirmatn", sans-serif;

  font-weight: 700;

  letter-spacing: -0.04em;

  line-height: 1.16;

  text-align: right;
}

.lang-fa .hero-title {
  font-size: clamp(56px, 5.15vw, 76px);
}

.lang-fa .hero-title strong {
  font-weight: 700;
}

.lang-fa .hero-title-accent,
.lang-fa .display-title em {
  font-style: normal;

  font-weight: 800;

  color: var(--accent);
}

.lang-fa .eyebrow,
.lang-fa .section-caption {
  letter-spacing: 0;
}

.lang-fa .hero-description,
.lang-fa .service-body p,
.lang-fa .about-content p,
.lang-fa .expertise-content p,
.lang-fa .testimonial-card__box p,
.lang-fa .contact-card p,
.lang-fa .cta-panel p,
.lang-fa .footer-brand-block p {
  line-height: 2;

  text-align: right;

  font-size: 14px;
}

.lang-fa .hero-actions {
  direction: rtl;

  justify-content: flex-start;
}

.lang-fa .hero-round-button span,
.lang-fa .hero-link,
.lang-fa .talk-arrow,
.lang-fa .menu-arrow,
.lang-fa .project-arrow,
.lang-fa .services-work-link strong,
.lang-fa .pill-link strong {
  direction: ltr;
}

.lang-fa .product-card {
  right: auto;

  left: 0;

  border-left: 1px solid rgba(255, 255, 255, 0.78);

  border-right: 0;

  text-align: right;
}

.lang-fa .hero-stats {
  right: auto;

  left: 0;

  border-left: 0;

  border-right: 1px solid var(--accent);

  border-radius: 14px 0 0 14px;

  text-align: right;
}

.lang-fa .hero-stats .stat-item {
  text-align: right;
}

.lang-fa .footer-columns {
  direction: rtl;
}

.lang-fa .footer-bottom {
  direction: rtl;
}

.lang-fa .footer-social {
  direction: rtl;
}

.lang-fa .footer-social select {
  direction: rtl;
}

.lang-fa .footer-brand-block {
  direction: rtl;

  text-align: right;
}

.lang-fa .service-item {
  padding-left: 24px;

  padding-right: 17px;

  border-right: 0;

  border-left: 1px solid var(--line);
}

.lang-fa .service-item .service-number {
  text-align: right;
}

.lang-fa .service-body {
  text-align: right;
}

.lang-fa .testimonial-card__box p {
  padding-right: 0;

  padding-left: 20px;

  text-align: right;
}

.lang-fa .testimonial-quote {
  inset-inline-start: 24px;
  inset-inline-end: auto;
}

.lang-fa .testimonial-client {
  padding-left: 0;

  padding-right: 5px;

  direction: rtl;
}

.lang-fa .testimonial-stars {
  direction: ltr;
}

.lang-fa .project-meta {
  direction: rtl;

  text-align: right;
}

.lang-fa .project-arrow {
  direction: ltr;
}

.lang-fa .contact-details {
  align-items: flex-start;
}

.lang-fa .contact-mail {
  direction: ltr;

  text-align: left;
}

/* =========================================================
   24. TABLET
========================================================= */

@media (max-width: 1180px) {
  .container {
    width: min(calc(100% - 46px), var(--container));
  }

  .desktop-nav {
    gap: 17px;
  }

  .hero-art {
    right: -235px;

    transform: translate3d(0, 0, 0) scale(0.9);

    transform-origin: top right;
  }

  .lang-fa .hero-art {
    right: auto;

    left: -235px;

    transform: translate3d(0, 0, 0) scale(0.9);

    transform-origin: top left;
  }

  .product-card {
    right: 0;
  }

  .lang-fa .product-card {
    right: auto;

    left: 0;
  }

  .hero-stats {
    right: 0;
  }

  .lang-fa .hero-stats {
    right: auto;

    left: 0;
  }

  .content-grid,
  .expertise-grid {
    gap: 40px;
  }

  .services-grid {
    grid-template-columns: repeat(2, 1fr);
  }

  .service-item:nth-child(3n) {
    border-right: 1px solid var(--line);
  }

  .service-item:nth-child(2n) {
    border-right: 0;
  }

  .lang-fa .service-item {
    border-right: 0;

    border-left: 1px solid var(--line);
  }

  .lang-fa .service-item:nth-child(2n) {
    border-left: 0;
  }

  .footer-top {
    gap: 50px;
  }
}

/* =========================================================
   25. 901 - 1024
========================================================= */

@media (min-width: 901px) and (max-width: 1024px) {
  .hero {
    min-height: 810px;
  }

  .hero-container {
    min-height: 665px;
  }

  .hero-copy {
    width: 470px;
  }

  .hero-title {
    font-size: clamp(62px, 7.1vw, 78px);
  }

  .lang-fa .hero-title {
    font-size: clamp(54px, 6.1vw, 70px);
  }

  .product-card {
    width: 210px;

    top: 58px;
  }

  .lang-fa .product-card {
    left: 0;
    right: auto;
  }

  .hero-stats {
    width: 165px;

    bottom: 38px;
  }

  .lang-fa .hero-stats {
    left: 0;
    right: auto;
  }

  .hero-art {
    right: -290px;

    transform: translate3d(0, 0, 0) scale(0.82);
  }

  .lang-fa .hero-art {
    right: auto;

    left: -290px;

    transform: translate3d(0, 0, 0) scale(0.82);
  }
}

/* =========================================================
   26. TABLET / MOBILE — <= 900
========================================================= */

@media (max-width: 900px) {
  .desktop-nav,
  .desktop-only {
    display: none;
  }

  .menu-toggle {
    display: block;
  }

  .hero {
    min-height: 900px;

    padding: 135px 0 40px;
  }

  .hero-container {
    min-height: 775px;
  }

  .hero-copy {
    width: 100%;

    max-width: 100%;
  }

  .hero-title {
    max-width: 650px;

    font-size: clamp(60px, 9.2vw, 84px);
  }

  .lang-fa .hero-title {
    max-width: 650px;

    font-size: clamp(54px, 8.1vw, 78px);
  }

  .hero-description {
    width: min(100%, 390px);
  }

  .hero-art {
    --art-scale: 0.72;

    top: 355px;

    right: -225px;

    left: auto;

    width: 850px;
    height: 590px;

    transform: translate3d(0, 0, 0) scale(var(--art-scale));

    transform-origin: top right;
  }

  .lang-fa .hero-art {
    --art-scale: 0.72;

    right: auto;

    left: -225px;

    transform: translate3d(0, 0, 0) scale(var(--art-scale));

    transform-origin: top left;
  }

  .site-shell.page-ready .hero-art {
    animation: heroArtEntryMobile 1.15s 0.1s cubic-bezier(0.22, 1, 0.36, 1) both;
  }

  .site-shell.page-ready.lang-fa .hero-art {
    animation: heroArtEntryMobileFa 1.15s 0.1s cubic-bezier(0.22, 1, 0.36, 1)
      both;
  }

  .product-card {
    top: 295px;

    right: 0;

    left: auto;

    width: min(220px, 31vw);

    padding: 15px 16px;
  }

  .lang-fa .product-card {
    right: auto;

    left: 0;
  }

  .hero-card-title {
    gap: 8px;

    line-height: 1.5;
  }

  .hero-card-title > span:last-child {
    font-size: 12px;

    line-height: 1.5;
  }

  .product-card p {
    margin: 11px 0 19px;

    font-size: 10px;

    line-height: 1.75;
  }

  .hero-stats {
    right: 0;

    left: auto;

    bottom: 10px;

    width: 165px;

    padding: 12px 15px;
  }

  .lang-fa .hero-stats {
    right: auto;

    left: 0;
  }

  .stat-item + .stat-item {
    margin-top: 15px;
  }

  .stat-item strong {
    font-size: 15px;
  }

  .stat-item span {
    font-size: 7.5px;
  }

  .scroll-rail {
    display: none;
  }

  .content-grid,
  .expertise-grid,
  .work-top,
  .contact-wrapper,
  .cta-panel {
    grid-template-columns: 1fr;
  }

  .content-grid,
  .expertise-grid {
    gap: 32px;
  }

  .work-top {
    gap: 32px;
  }

  .contact-wrapper {
    gap: 45px;
  }

  .cta-panel {
    gap: 35px;

    align-items: start;
  }

  .testimonials-grid {
    grid-template-columns: 1fr;
  }

  .footer-top {
    grid-template-columns: 1fr;

    gap: 45px;
  }

  .footer-columns {
    grid-template-columns: repeat(3, 1fr);
  }

  .lang-fa .contact-wrapper,
  .lang-fa .content-grid,
  .lang-fa .expertise-grid,
  .lang-fa .work-top,
  .lang-fa .cta-panel {
    direction: rtl;
  }

  .lang-fa .service-item,
  .lang-fa .service-item:nth-child(3n),
  .lang-fa .service-item:nth-child(2n) {
    border-right: 0;

    border-left: 1px solid var(--line);
  }

  .lang-fa .service-item:nth-child(2n) {
    border-left: 0;
  }

  .to-top {
    right: 25px;

    left: auto;
  }

  .lang-fa .to-top {
    right: auto;

    left: 25px;
  }
}

/* =========================================================
   27. 768 - 900
========================================================= */

@media (min-width: 768px) and (max-width: 900px) {
  .hero {
    min-height: 900px;
  }

  .hero-art {
    --art-scale: 0.72;

    top: 375px;

    right: -235px;
  }

  .lang-fa .hero-art {
    left: -235px;

    right: auto;
  }

  .product-card {
    top: 300px;

    width: 225px;
  }

  .lang-fa .product-card {
    left: 0;

    right: auto;
  }

  .hero-stats {
    bottom: 20px;

    width: 170px;
  }

  .lang-fa .hero-stats {
    left: 0;

    right: auto;
  }

  .hero-title::before {
    top: 12px;
  }

  .hero-title::after {
    top: 4px;
  }
}

/* =========================================================
   28. MOBILE — <= 640
========================================================= */

@media (max-width: 640px) {
  .container {
    width: calc(100% - 32px);
  }

  .site-header {
    padding: 20px 0;
  }

  .brand {
    gap: 8px;
  }

  .brand-name {
    font-size: 11px;
  }

  .lang-fa .brand-name {
    font-size: 14px;
  }

  .language-switch {
    font-size: 9px;
  }

  .header-actions {
    gap: 14px;
  }

  .mobile-menu-panel {
    width: min(440px, 92vw);

    padding: 90px 24px 26px;
  }

  .mobile-menu-panel nav a {
    font-size: 22px;
  }

  .hero {
    min-height: 850px;

    padding: 117px 0 40px;
  }

  .hero-container {
    min-height: 720px;
  }

  .eyebrow,
  .section-caption {
    gap: 12px;

    font-size: 12px;
  }

  .eyebrow i,
  .section-caption i {
    width: 33px;
  }

  .hero-title {
    max-width: 100%;

    margin: 25px 0 24px;

    font-size: clamp(50px, 13.6vw, 70px);

    line-height: 1;
  }

  .lang-fa .hero-title {
    max-width: 100%;

    font-size: clamp(47px, 12.4vw, 64px);

    line-height: 1.2;
  }

  .hero-description {
    width: min(100%, 320px);

    font-size: 12px;

    line-height: 1.9;
  }

  .lang-fa .hero-description {
    width: min(100%, 320px);
  }

  .hero-actions {
    gap: 14px;

    margin-top: 24px;
  }

  .hero-round-button {
    width: 47px;
    height: 47px;
  }

  .hero-link {
    font-size: 10px;
  }

  .hero-divider {
    width: 30px;

    margin-left: 2px;
  }

  .hero-art {
    --art-scale: 0.58;

    top: 355px;

    right: -218px;

    left: auto;

    width: 800px;
    height: 590px;

    transform: translate3d(0, 0, 0) scale(var(--art-scale));

    transform-origin: top right;
  }

  .lang-fa .hero-art {
    --art-scale: 0.58;

    right: auto;

    left: -218px;

    transform: translate3d(0, 0, 0) scale(var(--art-scale));

    transform-origin: top left;
  }

  .product-card {
    top: 315px;

    right: 0;

    left: auto;

    width: min(188px, 47vw);

    padding: 13px 14px;
  }

  .lang-fa .product-card {
    right: auto;

    left: 0;
  }

  .hero-card-title {
    gap: 7px;

    line-height: 1.55;
  }

  .hero-card-title > span:last-child {
    font-size: 11px;

    line-height: 1.55;
  }

  .status-dot {
    width: 7px;
    height: 7px;

    flex-basis: 7px;

    margin-top: 4px;
  }

  .product-card p {
    margin: 10px 0 17px;

    font-size: 9px;

    line-height: 1.75;
  }

  .hero-card-footer {
    min-height: 14px;
  }

  .hero-card-footer i {
    width: 30px;
  }

  .hero-stats {
    right: 0;

    left: auto;

    bottom: 2px;

    width: 155px;

    padding: 11px 13px;
  }

  .lang-fa .hero-stats {
    right: auto;

    left: 0;

    transform-origin: bottom left;
  }

  .stat-item + .stat-item {
    margin-top: 13px;
  }

  .stat-item strong {
    font-size: 14px;
  }

  .stat-item span {
    font-size: 6.5px;

    line-height: 1.5;
  }

  .about,
  .expertise,
  .testimonials {
    padding: 95px 0;
  }

  .services {
    padding: 48px 0 84px;
  }

  .services-grid {
    grid-template-columns: 1fr;
  }

  .service-item,
  .service-item:nth-child(3n),
  .service-item:nth-child(2n) {
    min-height: auto;

    padding: 19px 0;

    border-right: 0;

    border-left: 0;
  }

  .lang-fa .service-item,
  .lang-fa .service-item:nth-child(3n),
  .lang-fa .service-item:nth-child(2n) {
    border-right: 0;

    border-left: 0;
  }

  .service-body h2 {
    font-size: 14px;

    max-width: 100%;
  }

  .service-body p {
    max-width: 100%;

    font-size: 11px;

    line-height: 1.8;
  }

  .lang-fa .service-body p {
    font-size: 12px;
  }

  .services-work-link {
    justify-content: flex-start;

    min-height: 90px;
  }

  .display-title {
    font-size: clamp(47px, 13vw, 68px);
  }

  .lang-fa .display-title {
    font-size: clamp(44px, 12.2vw, 64px);
  }

  .work {
    padding: 90px 0 100px;
  }

  .work-top {
    margin-bottom: 40px;
  }

  .work-grid {
    grid-template-columns: 1fr;

    gap: 40px;
  }

  .project-large {
    grid-column: auto;
  }

  .project-visual,
  .project-large .project-visual {
    min-height: 280px;
  }

  .project-large .project-visual {
    min-height: 330px;
  }

  .project-meta h3 {
    font-size: 13px;

    line-height: 1.55;
  }

  .about-stats {
    gap: 10px;
  }

  .about-stat strong {
    font-size: 23px;
  }

  .about-stat span {
    font-size: 8px;
  }

  .expertise-tags {
    gap: 7px;
  }

  .expertise-tags span {
    padding: 9px 12px;

    font-size: 9px;
  }

  .testimonial-card__box {
    min-height: auto;

    padding: 24px;
  }

  .testimonial-card__box p {
    padding-right: 0;

    font-size: 12px;

    line-height: 2;
  }

  .lang-fa .testimonial-card__box p {
    padding-left: 0;

    padding-right: 0;

    font-size: 12px;
  }

  .testimonial-quote {
    top: 105px;

    inset-inline-end: 18px;

    font-size: 52px;
  }

  .lang-fa .testimonial-quote {
    inset-inline-start: 18px;

    inset-inline-end: auto;
  }

  .testimonial-client {
    padding-left: 4px;

    gap: 11px;
  }

  .lang-fa .testimonial-client {
    padding-right: 4px;

    padding-left: 0;
  }

  .testimonial-client strong {
    font-size: 10px;
  }

  .testimonial-client span {
    font-size: 8.5px;
  }

  .cta {
    padding: 60px 0 95px;
  }

  .cta-panel {
    min-height: auto;

    padding: 32px 26px 36px;

    border-radius: 20px;
  }

  .cta-panel p {
    font-size: 12px;

    line-height: 2;
  }

  .pill-link {
    width: fit-content;

    font-size: 10px;
  }

  .contact {
    padding: 90px 0 105px;
  }

  .contact-cards {
    grid-template-columns: 1fr;

    margin-top: 34px;
  }

  .contact-card {
    padding: 21px;
  }

  .contact-card p {
    font-size: 10px;

    line-height: 1.9;
  }

  .lang-fa .contact-card p {
    font-size: 11px;
  }

  .contact-details a {
    font-size: 10px;
  }

  .contact-visual {
    min-height: 390px;

    border-radius: 24px;
  }

  .contact-sphere {
    width: 145px;
    height: 145px;
  }

  .orbit-contact-1 {
    width: 320px;
    height: 145px;
  }

  .orbit-contact-2 {
    width: 270px;
    height: 120px;
  }

  .contact-mail {
    bottom: 29px;

    font-size: 9px;
  }

  .footer {
    padding: 44px 0 25px;
  }

  .footer-columns {
    grid-template-columns: 1fr;

    gap: 10px;
  }

  .footer-col {
    border-bottom: 1px solid var(--line);
  }

  .footer-col__toggle {
    padding: 13px 0;

    font-size: 10px;
  }

  .footer-col__arrow {
    display: block;

    color: #87909d;

    font-size: 15px;

    transition: transform 0.3s ease;
  }

  .footer-col.is-open .footer-col__arrow {
    transform: rotate(180deg);
  }

  .footer-col__links {
    max-height: 0;

    margin: 0;

    padding: 0;

    overflow: hidden;

    opacity: 0;

    pointer-events: none;

    transition:
      max-height 0.4s ease,
      opacity 0.3s ease,
      padding 0.4s ease;
  }

  .footer-col.is-open .footer-col__links {
    max-height: 300px;

    padding: 3px 0 18px;

    opacity: 1;

    pointer-events: auto;
  }

  .footer-col__links a {
    font-size: 10px;
  }

  .footer-bottom {
    flex-direction: column;

    align-items: stretch;

    gap: 18px;
  }

  .footer-social {
    justify-content: space-between;

    gap: 14px;
  }

  .footer-social select {
    min-width: 105px;
  }

  .to-top {
    right: 17px;

    left: auto;

    bottom: 17px;

    width: 39px;
    height: 39px;
  }

  .lang-fa .to-top {
    right: auto;

    left: 17px;
  }

  .hero-title::before {
    top: 1px;

    width: 38px;
    height: 38px;
  }

  .hero-title::after {
    top: -7px;

    width: 50px;
    height: 50px;
  }

  .lang-fa .hero-title::before {
    left: 4%;

    right: auto;
  }

  .lang-fa .hero-title::after {
    left: -3px;

    right: auto;
  }
}

/* =========================================================
   29. 480 - 640
========================================================= */

@media (min-width: 481px) and (max-width: 640px) {
  .hero {
    min-height: 875px;
  }

  .hero-container {
    min-height: 745px;
  }

  .hero-art {
    --art-scale: 0.6;

    top: 355px;

    right: -225px;
  }

  .lang-fa .hero-art {
    left: -225px;

    right: auto;
  }

  .product-card {
    width: min(195px, 39vw);

    top: 315px;
  }

  .lang-fa .product-card {
    left: 0;

    right: auto;
  }

  .hero-stats {
    width: 160px;
  }

  .lang-fa .hero-stats {
    left: 0;

    right: auto;
  }
}

/* =========================================================
   30. VERY SMALL MOBILE — <= 420
========================================================= */

@media (max-width: 420px) {
  .container {
    width: calc(100% - 26px);
  }

  .site-header {
    padding: 17px 0;
  }

  .header-actions {
    gap: 11px;
  }

  .brand-name {
    font-size: 10px;
  }

  .lang-fa .brand-name {
    font-size: 13px;
  }

  .language-switch {
    font-size: 8px;
  }

  .mobile-menu-panel {
    padding: 84px 21px 24px;
  }

  .hero {
    min-height: 815px;

    padding-top: 110px;
  }

  .hero-container {
    min-height: 690px;
  }

  .hero-title {
    font-size: 48px;

    line-height: 1;
  }

  .lang-fa .hero-title {
    font-size: 46px;

    line-height: 1.2;
  }

  .hero-description {
    max-width: 285px;

    font-size: 11px;
  }

  .lang-fa .hero-description {
    font-size: 11px;
  }

  .hero-actions {
    gap: 11px;
  }

  .hero-round-button {
    width: 44px;
    height: 44px;
  }

  .hero-link {
    font-size: 9px;
  }

  .hero-divider {
    width: 23px;
  }

  .hero-art {
    --art-scale: 0.52;

    top: 338px;

    right: -207px;

    left: auto;

    transform: translate3d(0, 0, 0) scale(var(--art-scale));

    transform-origin: top right;
  }

  .lang-fa .hero-art {
    --art-scale: 0.52;

    right: auto;

    left: -207px;

    transform: translate3d(0, 0, 0) scale(var(--art-scale));

    transform-origin: top left;
  }

  .product-card {
    top: 306px;

    right: 0;

    left: auto;

    width: min(164px, 44vw);

    padding: 11px;
  }

  .lang-fa .product-card {
    right: auto;

    left: 0;
  }

  .hero-card-title {
    gap: 6px;
  }

  .hero-card-title > span:last-child {
    font-size: 9.5px;

    line-height: 1.55;
  }

  .status-dot {
    width: 6px;
    height: 6px;

    flex-basis: 6px;

    margin-top: 3px;
  }

  .product-card p {
    margin: 8px 0 14px;

    font-size: 8px;

    line-height: 1.7;
  }

  .hero-card-footer i {
    width: 26px;
  }

  .hero-stats {
    right: 0;

    left: auto;

    bottom: 0;

    width: 145px;

    padding: 10px 12px;
  }

  .lang-fa .hero-stats {
    right: auto;

    left: 0;
  }

  .stat-item + .stat-item {
    margin-top: 11px;
  }

  .stat-item strong {
    font-size: 13px;
  }

  .stat-item span {
    font-size: 6px;
  }

  .hero-title::before {
    top: -1px;

    width: 32px;
    height: 32px;

    border-radius: 11px;
  }

  .hero-title::after {
    top: -7px;

    width: 43px;
    height: 43px;
  }

  .lang-fa .hero-title::before {
    left: 4%;

    right: auto;
  }

  .lang-fa .hero-title::after {
    left: -2px;

    right: auto;
  }

  .display-title {
    font-size: 43px;
  }

  .lang-fa .display-title {
    font-size: 41px;
  }

  .project-visual,
  .project-large .project-visual {
    min-height: 255px;
  }

  .contact-title {
    font-size: 45px;
  }

  .contact-visual {
    min-height: 360px;
  }

  .contact-sphere {
    width: 132px;
    height: 132px;
  }

  .orbit-contact-1 {
    width: 285px;
    height: 130px;
  }

  .orbit-contact-2 {
    width: 235px;
    height: 105px;
  }

  .contact-mail {
    max-width: calc(100% - 28px);

    font-size: 8px;
  }

  .footer-social {
    flex-wrap: wrap;
  }

  .footer-social select {
    min-width: 100px;
  }

  .loader-label {
    bottom: 40px;
  }

  .loader-core {
    width: 64px;
    height: 64px;
  }
}

/* =========================================================
   30-B. HERO CARDS IN FLOW — <= 800px
========================================================= */

@media (max-width: 800px) {
  .hero-container {
    display: flex;

    flex-direction: column;

    align-items: stretch;
  }

  .hero-copy {
    order: 1;

    width: 100%;

    max-width: 100%;
  }

  .hero-cards {
    order: 2;

    position: relative;

    z-index: 40;

    display: grid;

    grid-template-columns: repeat(auto-fit, minmax(148px, 1fr));

    align-items: stretch;

    gap: 12px;

    width: 100%;

    margin-top: 34px;
  }

  .product-card,
  .lang-fa .product-card,
  .hero-stats,
  .lang-fa .hero-stats {
    position: static;

    inset: auto;

    top: auto;
    right: auto;
    bottom: auto;
    left: auto;

    width: auto;

    max-width: none;

    min-width: 0;

    height: auto;

    margin: 0;

    padding: 18px;

    border: 1px solid rgba(255, 255, 255, 0.88);

    border-radius: 18px;

    background: rgba(255, 255, 255, 0.7);

    box-shadow: 0 16px 40px rgba(61, 71, 105, 0.08);

    text-align: start;

    backdrop-filter: blur(18px);
    -webkit-backdrop-filter: blur(18px);
  }

  .hero-stats,
  .lang-fa .hero-stats {
    display: flex;

    flex-direction: column;

    justify-content: center;

    border-inline-start: 2px solid var(--accent);

    border-radius: 18px;
  }

  .hero-stats .stat-item,
  .lang-fa .hero-stats .stat-item {
    text-align: start;
  }

  .stat-item + .stat-item {
    margin-top: 14px;
  }

  .hero-card-title > span:last-child {
    font-size: clamp(11px, 1.6vw, 14px);
  }

  .product-card p {
    margin: 12px 0 18px;

    font-size: clamp(9px, 1.35vw, 12px);

    line-height: 1.75;
  }

  .stat-item strong {
    font-size: clamp(14px, 2vw, 18px);
  }

  .stat-item span {
    font-size: clamp(7.5px, 1vw, 10px);

    line-height: 1.5;
  }
}

/* =========================================================
   31. REDUCED MOTION
========================================================= */

@media (prefers-reduced-motion: reduce) {
  html {
    scroll-behavior: auto;
  }

  *,
  *::before,
  *::after {
    animation-duration: 0.001ms !important;

    animation-iteration-count: 1 !important;

    transition-duration: 0.001ms !important;

    scroll-behavior: auto !important;
  }
}
</style>
