<template>
  <section class="word-adventure-page" aria-labelledby="word-adventure-title">
    <button class="back-button" type="button" aria-label="返回主页" @click="emit('back-home')">
      <span aria-hidden="true">←</span>
    </button>

    <section class="hero">
      <div class="terrain" aria-hidden="true">
        <div class="cloud cloud-a" />
        <div class="cloud cloud-b" />
        <div class="path" />
        <div class="checkpoint checkpoint-a">
          <img src="/images/word-adventure/key.png" alt="" />
        </div>
        <div class="checkpoint checkpoint-b">
          <img src="/images/word-adventure/book.png" alt="" />
        </div>
        <div class="checkpoint checkpoint-c">
          <img src="/images/word-adventure/unlock.png" alt="" />
        </div>
        <img class="hero-img" src="/images/word-adventure/hero.png" alt="" />
        <img class="snake-img" src="/images/word-adventure/pixel_snake.png" alt="" />
        <img class="monster-img monster-a" src="/images/word-adventure/monster1_idle.png" alt="" />
        <img class="monster-img monster-b" src="/images/word-adventure/monster2_idle.png" alt="" />
      </div>

      <div class="hero-copy">
        <p class="eyebrow">Recite Words Adventure</p>
        <h1 id="word-adventure-title">单词大冒险</h1>
        <p class="lead">
          把每天要背的单词变成一段闯关旅程：勇者前进、怪物拦路、钥匙解锁，复习和新学都更有游戏感。
        </p>
        <div class="hero-actions">
          <button class="primary-action" type="button" @click="scrollToSection('adventure-preview')">
            <img src="/images/word-adventure/hero.png" alt="" />
            <span>查看玩法</span>
          </button>
          <button class="secondary-action" type="button" @click="scrollToSection('adventure-features')">
            了解亮点
          </button>
        </div>
      </div>
    </section>

    <section id="adventure-preview" class="section preview-section">
      <div class="phone-shell">
        <div class="phone-screen">
          <div class="app-top">
            <span>复习 6/10</span>
            <span>新学 3/15</span>
          </div>
          <div class="progress-line">
            <img src="/images/word-adventure/hero.png" alt="" />
            <img src="/images/word-adventure/pixel_monster.png" alt="" />
          </div>
          <div class="word-card">
            <span class="word">adventure</span>
            <span class="phonetic">/ədˈventʃər/</span>
          </div>
          <div class="choice-list">
            <button type="button">
              <img src="/images/word-adventure/monster1_idle.png" alt="" />
              <span>冒险；奇遇</span>
            </button>
            <button type="button">
              <img src="/images/word-adventure/monster2_idle.png" alt="" />
              <span>天气；气候</span>
            </button>
            <button type="button">
              <img src="/images/word-adventure/monster3_idle.png" alt="" />
              <span>节奏；速度</span>
            </button>
          </div>
        </div>
      </div>
      <div class="preview-copy">
        <span class="section-kicker">Daily Quest</span>
        <h2>今天的单词，就是今天的地图</h2>
        <p>
          页面围绕“每日任务”组织信息：当前词书、学习进度、复习任务和闯关入口一眼可见，适合给产品做一个清爽的展示入口。
        </p>
      </div>
    </section>

    <section id="adventure-features" class="section feature-section">
      <div class="section-heading">
        <span class="section-kicker">Highlights</span>
        <h2>轻量、直观、带一点像素冒险味</h2>
      </div>
      <div class="feature-grid">
        <article v-for="feature in features" :key="feature.title" class="feature-item">
          <img :src="feature.icon" alt="" />
          <h3>{{ feature.title }}</h3>
          <p>{{ feature.text }}</p>
        </article>
      </div>
    </section>
  </section>
</template>

<script setup>
const emit = defineEmits(["back-home"]);
const props = defineProps({
  initialSection: {
    type: String,
    default: "",
  },
});

const scrollToSection = (id) => {
  document.getElementById(id)?.scrollIntoView({
    behavior: "smooth",
    block: "start",
  });
};

const scrollToInitialSection = () => {
  if (!props.initialSection) return;
  nextTick(() => {
    window.setTimeout(() => scrollToSection(props.initialSection), 80);
  });
};

onMounted(scrollToInitialSection);

watch(
  () => props.initialSection,
  () => scrollToInitialSection(),
);

const features = [
  {
    icon: "/images/word-adventure/book.png",
    title: "词书进度",
    text: "已学数量和总词量集中展示，用户知道自己正在推进哪一本书。",
  },
  {
    icon: "/images/word-adventure/key.png",
    title: "闯关练习",
    text: "选择释义、拼写补全、复习回合都包装成不同关卡。",
  },
  {
    icon: "/images/word-adventure/word_collection.png",
    title: "生词沉淀",
    text: "遇到难词可以加入生词本，后续复习更有针对性。",
  },
];
</script>

<style lang="scss" scoped>
.word-adventure-page {
  position: fixed;
  inset: 0;
  z-index: 5;
  overflow-x: hidden;
  overflow-y: auto;
  color: #ffffff;
  background:
    linear-gradient(180deg, rgba(21, 71, 93, 0.95) 0%, rgba(28, 79, 73, 0.98) 42%, #152c39 100%),
    #152c39;
  scroll-behavior: smooth;
}

.back-button {
  position: fixed;
  top: 22px;
  left: 24px;
  z-index: 20;
  width: 44px;
  height: 44px;
  border: 1px solid rgba(255, 255, 255, 0.22);
  border-radius: 8px;
  background: rgba(9, 24, 31, 0.62);
  color: #ffffff;
  font-size: 22px;
  line-height: 1;
  cursor: pointer;
  backdrop-filter: blur(12px);
}

.hero {
  position: relative;
  min-height: 92dvh;
  padding: 12vh clamp(24px, 8vw, 120px) 10vh;
  display: flex;
  align-items: center;
  overflow: hidden;
  isolation: isolate;

  &::before {
    content: "";
    position: absolute;
    inset: 0;
    z-index: -3;
    background:
      linear-gradient(rgba(255, 255, 255, 0.05) 1px, transparent 1px),
      linear-gradient(90deg, rgba(255, 255, 255, 0.05) 1px, transparent 1px);
    background-size: 34px 34px;
    mask-image: linear-gradient(180deg, #000 0%, transparent 78%);
  }

  &::after {
    content: "";
    position: absolute;
    left: 0;
    right: 0;
    bottom: 0;
    height: 28vh;
    z-index: 0;
    background:
      linear-gradient(135deg, transparent 25%, rgba(255, 255, 255, 0.08) 25% 50%, transparent 50% 75%, rgba(255, 255, 255, 0.08) 75%),
      linear-gradient(180deg, #315f3c 0%, #24462f 100%);
    background-size: 36px 36px, 100% 100%;
    clip-path: polygon(0 35%, 10% 22%, 23% 34%, 35% 18%, 48% 32%, 60% 18%, 74% 31%, 88% 20%, 100% 32%, 100% 100%, 0 100%);
  }
}

.terrain {
  position: absolute;
  inset: 0;
  z-index: 1;
  pointer-events: none;
}

.hero-copy {
  position: relative;
  z-index: 2;
}

.cloud {
  position: absolute;
  height: 34px;
  border-radius: 8px;
  background: rgba(255, 255, 255, 0.24);
  box-shadow:
    36px 0 rgba(255, 255, 255, 0.24),
    72px 0 rgba(255, 255, 255, 0.24),
    18px -18px rgba(255, 255, 255, 0.24),
    54px -18px rgba(255, 255, 255, 0.24);
}

.cloud-a {
  top: 16%;
  right: 18%;
  width: 74px;
}

.cloud-b {
  top: 28%;
  right: 44%;
  width: 56px;
  transform: scale(0.78);
}

.path {
  position: absolute;
  right: 4vw;
  bottom: 8vh;
  width: min(58vw, 780px);
  height: 46vh;
  border-bottom: 22px solid rgba(222, 190, 122, 0.78);
  border-left: 18px solid transparent;
  border-radius: 0 0 0 44%;
  transform: rotate(-9deg);
}

.checkpoint {
  position: absolute;
  width: 62px;
  height: 62px;
  display: grid;
  place-items: center;
  border: 2px solid rgba(255, 255, 255, 0.28);
  border-radius: 10px;
  background: rgba(14, 36, 36, 0.64);
  box-shadow: 0 14px 30px rgba(0, 0, 0, 0.25);

  img {
    width: 36px;
    image-rendering: pixelated;
  }
}

.checkpoint-a {
  right: 33vw;
  bottom: 18vh;
}

.checkpoint-b {
  right: 17vw;
  bottom: 31vh;
}

.checkpoint-c {
  right: 9vw;
  bottom: 15vh;
}

.hero-img,
.snake-img,
.monster-img {
  position: absolute;
  image-rendering: pixelated;
}

.hero-img {
  right: min(44vw, 560px);
  bottom: 21vh;
  width: clamp(56px, 8vw, 92px);
  filter: drop-shadow(0 18px 20px rgba(0, 0, 0, 0.35));
  animation: float-step 2.8s ease-in-out infinite;
}

.snake-img {
  right: 25vw;
  bottom: 12vh;
  width: clamp(74px, 11vw, 132px);
  filter: drop-shadow(0 12px 14px rgba(0, 0, 0, 0.28));
}

.monster-img {
  width: clamp(92px, 13vw, 160px);
  filter: drop-shadow(0 18px 18px rgba(0, 0, 0, 0.32));
}

.monster-a {
  right: 10vw;
  bottom: 32vh;
}

.monster-b {
  right: 2vw;
  bottom: 10vh;
  transform: scaleX(-1);
}

.hero-copy {
  width: min(680px, 100%);
}

.eyebrow,
.section-kicker {
  display: inline-flex;
  align-items: center;
  margin-bottom: 16px;
  color: #ffe08a;
  font-size: 0.82rem;
  font-weight: 800;
  letter-spacing: 0;
  text-transform: uppercase;
}

h1,
h2,
h3,
p {
  text-shadow: 0 2px 14px rgba(0, 0, 0, 0.2);
}

h1 {
  max-width: 620px;
  font-size: clamp(3.2rem, 9vw, 7.6rem);
  line-height: 0.95;
}

.lead {
  max-width: 560px;
  margin-top: 26px;
  color: rgba(255, 255, 255, 0.86);
  font-size: clamp(1rem, 2vw, 1.35rem);
  line-height: 1.8;
}

.hero-actions {
  display: flex;
  flex-wrap: wrap;
  gap: 14px;
  margin-top: 34px;
}

.primary-action,
.secondary-action {
  min-height: 48px;
  display: inline-flex;
  align-items: center;
  justify-content: center;
  border-radius: 8px;
  font-weight: 700;
  text-decoration: none;
}

.primary-action {
  gap: 10px;
  padding: 0 22px;
  background: #ffe08a;
  color: #173342;
  box-shadow: 0 14px 30px rgba(0, 0, 0, 0.24);

  img {
    width: 28px;
    image-rendering: pixelated;
  }

  span {
    color: #173342;
  }
}

.secondary-action {
  padding: 0 20px;
  border: 1px solid rgba(255, 255, 255, 0.24);
  background: rgba(255, 255, 255, 0.08);
  backdrop-filter: blur(10px);
}

.section {
  width: min(1120px, calc(100% - 40px));
  margin: 0 auto;
  padding: 84px 0;
}

.preview-section {
  display: grid;
  grid-template-columns: minmax(280px, 430px) minmax(0, 1fr);
  gap: clamp(36px, 7vw, 96px);
  align-items: center;
}

.phone-shell {
  width: min(100%, 390px);
  margin: 0 auto;
  padding: 12px;
  border: 1px solid rgba(255, 255, 255, 0.22);
  border-radius: 28px;
  background: #0c1820;
  box-shadow: 0 30px 80px rgba(0, 0, 0, 0.35);
}

.phone-screen {
  min-height: 590px;
  padding: 18px;
  border-radius: 20px;
  background:
    linear-gradient(180deg, rgba(122, 188, 142, 0.28), transparent 34%),
    #f7f1df;

  * {
    color: #173342;
    text-shadow: none;
  }
}

.app-top {
  display: flex;
  justify-content: space-between;
  font-size: 0.9rem;
  font-weight: 800;
}

.progress-line {
  position: relative;
  height: 78px;
  margin: 24px 0;
  border-bottom: 8px solid #79a86f;

  img {
    position: absolute;
    bottom: 7px;
    image-rendering: pixelated;

    &:first-child {
      left: 24%;
      width: 42px;
    }

    &:last-child {
      right: 22%;
      width: 42px;
    }
  }
}

.word-card {
  padding: 28px 18px;
  border: 2px solid #163342;
  border-radius: 8px;
  background: #ffffff;
  text-align: center;
  box-shadow: 6px 6px 0 #d1b06a;

  .word {
    display: block;
    font-size: 2.1rem;
    font-weight: 900;
  }

  .phonetic {
    display: block;
    margin-top: 8px;
    color: #66757f;
  }
}

.choice-list {
  display: grid;
  gap: 12px;
  margin-top: 24px;

  button {
    min-height: 74px;
    padding: 10px 14px;
    display: flex;
    align-items: center;
    gap: 14px;
    border: 2px solid #163342;
    border-radius: 8px;
    background: #ffffff;
    font-size: 1rem;
    font-weight: 800;

    &:first-child {
      background: #d6f5d9;
    }
  }

  img {
    width: 56px;
    image-rendering: pixelated;
  }
}

.preview-copy {
  h2 {
    max-width: 620px;
    font-size: clamp(2rem, 4vw, 4.2rem);
    line-height: 1.08;
  }

  p {
    max-width: 560px;
    margin-top: 22px;
    color: rgba(255, 255, 255, 0.78);
    font-size: 1.05rem;
    line-height: 1.9;
  }
}

.feature-section {
  padding-top: 56px;
}

.section-heading {
  max-width: 720px;
  margin-bottom: 34px;

  h2 {
    font-size: clamp(1.8rem, 4vw, 3.5rem);
    line-height: 1.16;
  }
}

.feature-grid {
  display: grid;
  grid-template-columns: repeat(3, minmax(0, 1fr));
  gap: 18px;
}

.feature-item {
  min-height: 230px;
  padding: 28px;
  border: 1px solid rgba(255, 255, 255, 0.18);
  border-radius: 8px;
  background: rgba(255, 255, 255, 0.08);
  backdrop-filter: blur(12px);

  img {
    width: 48px;
    height: 48px;
    object-fit: contain;
    image-rendering: pixelated;
  }

  h3 {
    margin-top: 22px;
    font-size: 1.35rem;
  }

  p {
    margin-top: 12px;
    color: rgba(255, 255, 255, 0.74);
    line-height: 1.75;
  }
}

@keyframes float-step {
  0%,
  100% {
    transform: translateY(0);
  }
  50% {
    transform: translateY(-8px);
  }
}

@media (max-width: 900px) {
  .hero {
    min-height: 94dvh;
    padding: 96px 24px 42vh;
    align-items: flex-start;
  }

  .path {
    right: -14vw;
    bottom: 6vh;
    width: 116vw;
    height: 34vh;
  }

  .checkpoint-a {
    right: 58vw;
    bottom: 17vh;
  }

  .checkpoint-b {
    right: 30vw;
    bottom: 25vh;
  }

  .checkpoint-c {
    right: 8vw;
    bottom: 13vh;
  }

  .hero-img {
    right: 64vw;
    bottom: 22vh;
  }

  .snake-img {
    right: 34vw;
    bottom: 11vh;
  }

  .monster-a {
    right: 4vw;
    bottom: 25vh;
  }

  .monster-b {
    display: none;
  }

  .preview-section {
    grid-template-columns: 1fr;
  }

  .preview-copy {
    order: -1;
  }

  .feature-grid {
    grid-template-columns: 1fr;
  }
}

@media (max-width: 520px) {
  .back-button {
    top: 14px;
    left: 14px;
  }

  .hero {
    padding-top: 86px;
  }

  h1 {
    font-size: clamp(3rem, 16vw, 4.6rem);
  }

  .hero-actions {
    width: 100%;
  }

  .primary-action,
  .secondary-action {
    width: 100%;
  }

  .section {
    width: min(100% - 28px, 1120px);
    padding: 58px 0;
  }

  .phone-screen {
    min-height: 520px;
    padding: 14px;
  }
}
</style>
