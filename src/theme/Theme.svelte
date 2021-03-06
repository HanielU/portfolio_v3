<style global>
  :root {
    --text_0: #343434;
    --text_1: #6f6f6f;
    --text_invert: #e2e2e2; /* similar to bg but lighter */
    --bg_0: #f8f3ef;
    --bg_1: #fff;
    --bg_invert: #2e2a2f; /* #same as .dark bg_1; */
    --bg_invert_transparent: #2e2a2f00; /* for safari... */

    --primary_1: #9b78de;
    --primary_1_smooth: #e9e1f8;
    --primary_1_highlight: #e9e1f8;
    --primary_1_sat: #8e66dc; /* better for small text */
    --primary_1_stronger: #8c00ff;
    --morph_color: rgba(172, 105, 255, 0.24);
    --morph_total: #c28ffc; /* visual effect when all circles are overlapping */
    --primary_2: #52e9d0;
    --primary_3: #dfb948;
    --primary_4: #ff9d9d;

    --error: #d52424;
  }

  body.dark {
    --text_0: #e2e2e2; /* same as --text_invert */
    --text_1: #adadad;
    --text_invert: #343434; /* same as defautl text_0 */
    --bg_0: #3a383b;
    --bg_1: #2e2a2f;
    --primary_1_sat: #a687ff;
    --primary_1_smooth: #514371;
    --primary_1_highlight: #8c00ff;
    --morph_color: rgba(159, 117, 255, 0.19);
    --morph_total: #8062be;
    --error: #ff9d9d;
  }

  /* ************************************ */

  html {
    font-size: 62.5%; /* 1rem = 10px */
  }

  body {
    background-color: var(--bg_0);
    color: var(--text_0);

    &.jsMotionDefault {
      /* smooth transition between themes */
      transition: color 0.2s ease-out, background-color 0.2s ease-out;
    }
    
    font-family: 'IBM Plex Sans', sans-serif;
    font-size: $font-M;
    line-height: 1.5;
    font-weight: 300;
    letter-spacing: 0.02em; /* visually better */

    /* avoid horizontal scroll when scrollbar is visible (windows) */
    width: 100vw;
    max-width: 100%;
    overflow-x: hidden;


    box-sizing: border-box;
    * { box-sizing: inherit; }
  }

  body.js-tabbing {
    a:focus,
    button:focus {
      outline: 0.1rem solid var(--primary_1_sat) !important;
      box-shadow: 0.2rem 0.2rem 0.2rem 0px var(--primary_1) !important;
    }
  }

  [tabindex="-1"]:focus {
    outline: none; /* it doesn't affect negatively Screen Readers */
  }

  /* ------ Text highlight ------ */
  ::selection {
    background: var(--primary_1_highlight);
  }
  ::-moz-selection {
    background: var(--primary_1_highlight);
  }

  /* ************************************ */

  .sr-only {
    position: absolute;
    width: 1px;
    height: 1px;
    padding: 0;
    margin: -1px;
    overflow: hidden;
    clip: rect(0, 0, 0, 0);
    border: 0;
  }

  /* ****** Font related ****** */
  .f-title {
    line-height: 1.2;
    font-weight: 500;
  }

  .f-bold {
    font-weight: 500;
  }

  /* Animation to show up...
  OPTIMIZE - centralize all "fadeins" around to use a unique global class */
  .uAppear {
    &-0,
    &-1 {
      opacity: 1;
      transition: opacity 200ms ease-in;

      /* OPTIMIZE avoid this?... */
      .uAppearSoon & {
        opacity: 0;
      }

      .uAppear & {
        transition: opacity 400ms ease-in;
      }
    }

    &-0 {
      .uAppear & {
        transition-delay: 50ms;
      }
    }

    &-1 {
      .uAppear & {
        transition-delay: 200ms;
      }
    }
  }

  .u-svg {
    /* this svg have an inline display: none; so in case the page is loaded without styles
    it doesn't ruin the layout. once styles are loaded, let's make sure we render this correctly */
    display: block !important;
  }

  .u-nowrap {
    white-space: nowrap;
  }

  .u-link {
    position: relative;

    text-decoration: underline;
    text-decoration-color: var(--primary_1);
    color: inherit;
    z-index: 0; /* so before gets behind but visible */

    &:hover {
      outline: none;
    }

    @media (--lg) { /* keep lg so long links work on "words" section */
      white-space: nowrap;

      .jsMotionDefault &:hover {
          &::before {
            transition-duration: 250ms ease-in-out;
            transform: scale(1, 1);
          }
      }

      &::before {
        content: '';
        position: absolute;
        bottom: 0.05em;
        left: -0.1em;
        width: calc(100% + 0.2em);
        height: 1.2em;
        background-color: var(--primary_1);
        opacity: 0.2;
        transform: scale(1, 0.3);
        transform-origin: 0 100%;
        z-index: -1;

        .jsMotionDefault & {
          transition: transform 75ms ease-out;
        }
      }
    }
  }
  
  .u-carousel {
    @media (--max-lg) { /* only used on mobile */
      width: 100vw;
      display: flex;
      overflow-x: auto;
      overflow-y: hidden;
      scroll-behavior: smooth;
      scroll-snap-type: x mandatory;
      overflow: scroll;
      -webkit-overflow-scrolling: touch;

      .u-carousel-item {
        position: relative;
        flex-shrink: 0;
        scroll-snap-align: center;
      }
    }
  }

  /* -------- Animations ------------- */

  @keyframes laserOn {
    0%,
    85% {
      opacity: 0;
    }
    87% {
      opacity: 0.8;
    }
    88% {
      opacity: 0.1;
    }
    89% {
      opacity: 0.8;
    }
    92% {
      opacity: 0.2;
    }
    94%,
    100% {
      opacity: 1;
    }
  }

  @keyframes fadeIn {
    0% {
      opacity: 0;
    }
    100% {
      opacity: 1;
    }
  }

  @keyframes fadeInWithPause {
    0% {
      opacity: 0;
    }
    40%, 100% {
      opacity: 1;
    }
  }
</style>