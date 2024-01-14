<script setup>
import { ref, onMounted } from 'vue';
import { gsap } from 'gsap';
import SplitType from 'split-type';

onMounted(() => {
  const ourText = new SplitType('h1', { types: 'chars' });
  const chars = ourText.chars;
  gsap.fromTo(
    chars,
    {
      y: 100,
      opacity: 0,
    },
    {
      y: 0,
      opacity: 1,
      stagger: 0.5,
      duration: 2,
      ease: 'power4.out',
    }
  );
});

// details start
import PlusIcon from './icons/Plus.vue';
import CloseIcon from './icons/CloseIcon.vue';

const showModal = ref(false);

const container = ref(null);
const text = ref(null);
const modal = ref(null);
const logo = ref(null);
const modalText = ref(null);
const icon = ref(null);
let tl = gsap.timeline();

const beforeEnter = (el) => {
  el.classList.add('animate');
};

const enter = (el, done) => {
  tl = gsap.timeline();

  const ourText = new SplitType('h1', { types: 'chars' });
  const chars = ourText.chars;

  tl.fromTo(
    icon.value.$el,
    {
      scale: 1,
    },
    {
      scale: 0.5,
      duration: 0.3,
      ease: 'back.inOut(1.7)',
    }
  )
    .to(
      icon.value.$el,
      {
        autoAlpha: 0.0,
        x: '9.5%',
        duration: 0.3,
        ease: 'back.out(1.7)',
      },
      '0'
    )
    .from(el, {
      //delay: 0.3,
      y: '-9%',
      x: '9.5%',
      scale: 0,
      scaleY: 2,
      borderRadius: '100%',
      transformOrigin: 'bottom left',
      duration: 0.5,
      ease: 'back.out(1.7)',
    })
    .fromTo(
      //logo.value,
      chars,
      {
        autoAlpha: 1,
        x: '0%',
      },
      {
        autoAlpha: 0,
        duration: 0.2,
        ease: 'back.out(1.7)',
        stagger: 0.0075,
      },
      '0.3'
    )
    .fromTo(
      modalText.value,
      {
        autoAlpha: 0,
        x: -50,
        y: 0,
      },
      {
        autoAlpha: 1,
        x: 0,
        y: 0,
        duration: 0.5,
        ease: 'circ.inOut',
      },
      '0.5'
    )
    .to(
      el,
      {
        scale: 1,
        scaleY: 1,
        duration: 0.15,
        ease: 'circ.inOut',
      },
      '+=0.075'
    );
};

const leave = (el, done) => {
  tl.reverse().then(done);
};
// details stop
</script>

<template>
  <div class="heading-details__container">
    <h1 ref="logo" class="font-didot box" id="heading">Explore</h1>

    <!-- details start -->
    <div class="details--container" @click="showModal = true" ref="container">
      <PlusIcon ref="icon" />
      <span font-lato ref="text">more details</span>
    </div>
  </div>

  <!-- modal start -->

  <transition name="fade" @before-enter="beforeEnter" @enter="enter" @leave="leave">
    <div v-if="showModal" class="p-4 explore--modal modal--container" ref="modal">
      <div>
        <div class="close--button" @click="showModal = false">
          <CloseIcon />
        </div>
        <div ref="modalText" class="text">
          <h2>explore</h2>
          <p>
            Sed ut perspiciatis unde omnis iste natus error sit voluptatem accusantium doloremque laudantium, totam rem
            aperiam, eaque ipsa quae ab illo inventore veritatis et quasi architecto beatae vitae dicta sunt explicabo.
            Nemo enim ipsam voluptatem quia voluptas sit aspernatur aut odit aut fugit, sed quia consequuntur magni
            dolores eos qui ratione voluptatem sequi nesciunt. Neque porro quisquam est, qui dolorem ipsum quia dolor
            sit amet, consectetur, adipisci velit, sed quia non numquam eius modi tempora incidunt ut labore et dolore
            magnam aliquam quaerat voluptatem. Ut enim ad minima veniam, quis nostrum exercitationem ullam corporis
            suscipit laboriosam, nisi ut aliquid ex ea commodi consequatur?
          </p>
          <button>read more</button>
        </div>
      </div>
    </div>
  </transition>
  <!-- modal stop -->
  <!-- details stop -->
</template>

<style scoped>
h1 {
  color: #ffffff;
  position: absolute;
  bottom: 23.4rem;
  left: 18.7rem;
  z-index: 2;
  font-size: 22.4rem;
  font-style: normal;
  font-weight: 700;
  line-height: normal;
  clip-path: polygon(0 0, 100% 0, 100% 100%, 0% 100%);
  overflow: hidden;
}
/* details start */
.heading-details__container {
  position: relative;
}
.details--container {
  display: flex;
  justify-content: center;
  align-items: center;
  gap: 2.2rem;
  position: absolute;
  bottom: 22.2rem;
  left: 18.7rem;
  z-index: 2;
  cursor: pointer;
}
span {
  text-transform: capitalize;
  color: #fff;
  text-align: center;
  font-family: Lato;
  font-size: 2.5rem;
  font-style: normal;
  font-weight: 400;
  line-height: normal;
  letter-spacing: 0.625px;
}
.explore--modal {
  position: absolute;
  margin-top: auto;
  margin-bottom: auto;
  left: 14rem;
  /* bottom: 17.3rem; */
  bottom: 0;
  top: 0;
  width: 58rem;
  height: 69rem;
  background: #fff;
  box-shadow: 0px 17px 25.3px 7px rgba(0, 0, 0, 0.1);
  padding: 7.2rem 7.2rem 7.8rem 6.6rem;
  z-index: 2;
}
.explore--modal .close--button {
  position: absolute;
  top: 2.5rem;
  right: 2.5rem;
  cursor: pointer;
}
.explore--modal h2 {
  color: #611818;
  font-family: Didot;
  font-size: 6.6rem;
  font-style: normal;
  font-weight: 700;
  line-height: normal;
  text-transform: capitalize;
}
.explore--modal p {
  margin-top: 2.6rem;
  margin-bottom: 2.9rem;
  color: #282828;
  font-family: Lato;
  font-size: 1.8rem;
  font-style: normal;
  font-weight: 400;
  line-height: 2.2rem; /* 122.222% */
  /* letter-spacing: 0.35px; */
  /* letter-spacing: 0.035rem; */
  letter-spacing: normal;
}
.explore--modal button {
  width: 23.5rem;
  height: 5.5rem;
  background: linear-gradient(90deg, #611818 0%, #a36754 100%);
  color: #fff;
  text-align: center;
  font-family: Lato;
  font-size: 1.8rem;
  font-style: normal;
  font-weight: 700;
  line-height: normal;
  letter-spacing: 1.693px;
  text-transform: uppercase;
}
.text {
  overflow: hidden;
}
@media (max-width: 480px) {
  #heading {
    bottom: 131.4rem;
  }
  .details--container {
    bottom: 130.2rem;
  }
}
/* details stop */
</style>
