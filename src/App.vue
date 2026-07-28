<script setup>
import { ref, computed } from 'vue'

const pitch = ref(0)
const speed = ref(1.0)
const isPlaying = ref(false)

const formatPitch = computed(() => {
  if (pitch.value === 0) return '원키 (0)'
  return pitch.value > 0 ? `+${pitch.value} 반음 (Key Up)` : `${pitch.value} 반음 (Key Down)`
})

const formatSpeed = computed(() => {
  return `${speed.value.toFixed(1)}x 배속`
})

const togglePlay = () => {
  isPlaying.value = !isPlaying.value
}

const resetControls = () => {
  pitch.value = 0
  speed.value = 1.0
}
</script>

<template>
  <div class="bg-decorations">
    <div class="orb orb-1"></div>
    <div class="orb orb-2"></div>
  </div>

  <div class="page-wrapper">
    <!-- Navigation Header -->
    <header class="header container">
      <div class="logo">
        <div class="logo-icon">🎵</div>
        <span class="logo-text">PitchPlayer</span>
      </div>
      <nav class="nav-links">
        <a href="#features">기능 소개</a>
        <a href="#demo">체험하기</a>
        <a href="./app-ads.txt" target="_blank" class="nav-badge">app-ads.txt</a>
      </nav>
    </header>

    <!-- Hero Section -->
    <section class="hero container">
      <div class="hero-content">
        <div class="badge">✨ 오프라인 로컬 음악 전용 플레이어</div>
        <h1 class="hero-title">
          음질 손실 없이 자유롭게<br />
          <span class="gradient-text">키(Pitch) & 속도(Tempo)</span> 조절
        </h1>
        <p class="hero-description">
          PitchPlayer는 내 기기에 저장된 음악 파일(MP3, FLAC 등)을 실시간 보컬 키 조절 및 템포 변경으로 재생해 주는 고성능 오프라인 뮤직 플레이어입니다.
        </p>
        <!-- <div class="hero-actions">
          <a href="#demo" class="btn btn-primary">
            <span>실시간 조절 데모</span>
            <svg width="20" height="20" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2.5"><path d="M5 12h14M12 5l7 7-7 7"/></svg>
          </a>
          <a href="#features" class="btn btn-secondary">주요 기능 둘러보기</a>
        </div> -->
      </div>

      <!-- Simulated Player Showcase -->
      <div class="hero-visual container" id="demo">
        <div class="glass-card player-mockup">
          <div class="player-header">
            <div class="track-info">
              <div class="track-album-art">🎧</div>
              <div>
                <div class="track-title">노래 연습 곡 (Demo Track)</div>
                <div class="track-artist">Pitch Player Engine</div>
              </div>
            </div>
            <button class="reset-btn" @click="resetControls" title="초기화">
              🔄 초기화
            </button>
          </div>

          <!-- Waveform Visualizer -->
          <div class="waveform-container">
            <div class="waveform-bars" :class="{ playing: isPlaying }">
              <span v-for="n in 28" :key="n" :style="{ animationDuration: `${(0.4 + (n % 5) * 0.15) / speed.value}s` }"></span>
            </div>
          </div>

          <!-- Controls Grid -->
          <div class="control-grid">
            <!-- Pitch Control -->
            <div class="control-item">
              <div class="control-label">
                <span>🎵 키 (Pitch)</span>
                <span class="control-value gradient-text">{{ formatPitch }}</span>
              </div>
              <input type="range" min="-6" max="6" step="1" v-model.number="pitch" class="slider" />
              <div class="slider-ticks">
                <span>-6</span>
                <span>0 (Original)</span>
                <span>+6</span>
              </div>
            </div>

            <!-- Tempo Control -->
            <div class="control-item">
              <div class="control-label">
                <span>⚡ 속도 (Tempo)</span>
                <span class="control-value gradient-text">{{ formatSpeed }}</span>
              </div>
              <input type="range" min="0.5" max="1.5" step="0.05" v-model.number="speed" class="slider" />
              <div class="slider-ticks">
                <span>0.5x</span>
                <span>1.0x</span>
                <span>1.5x</span>
              </div>
            </div>
          </div>

          <div class="player-footer">
            <button class="play-btn" @click="togglePlay">
              {{ isPlaying ? '⏸ 일시정지' : '▶ 재생하기' }}
            </button>
            <span class="engine-tag">Web Audio SoundTouch Engine</span>
          </div>
        </div>
      </div>
    </section>

    <!-- Features Section -->
    <section class="features-section container" id="features">
      <h2 class="section-title">왜 <span class="gradient-text">PitchPlayer</span>인가요?</h2>
      <div class="features-grid">
        <div class="glass-card feature-card">
          <div class="feature-icon">🎼</div>
          <h3>원음 정밀 키(Key) 조절</h3>
          <p>내 목소리 톤에 딱 맞게 보컬 반음/음정 조절 가능 (+-6 Key). 템포 변형 없이 깨끗한 사운드를 유지합니다.</p>
        </div>

        <div class="glass-card feature-card">
          <div class="feature-icon">⏱️</div>
          <h3>자유로운 배속 재생</h3>
          <p>0.5배속부터 1.5배속까지 0.05 단위 미세 속도 조절. 악기 연습이나 댄스 카피, 보컬 연습에 최적화되어 있습니다.</p>
        </div>

        <div class="glass-card feature-card">
          <div class="feature-icon">📂</div>
          <h3>오프라인 로컬 라이브러리</h3>
          <p>인터넷 연결 필요 없음! 기기 내 저장된 MP3, FLAC 오디오 파일 자동 스캔 및 즉시 재생 지원.</p>
        </div>

        <div class="glass-card feature-card">
          <div class="feature-icon">🔒</div>
          <h3>개인정보 보호 & 100% 로컬</h3>
          <p>사용자의 오디오 파일 및 데이터는 외부 서버로 절대 전송되지 않고 기기 내부에서 안전하게 실행됩니다.</p>
        </div>
      </div>
    </section>

    <!-- Footer -->
    <footer class="footer container">
      <div class="footer-content">
        <div class="footer-brand">
          <span class="logo-text">PitchPlayer</span>
          <p>로컬 음원 피치 및 템포 조절 음악 플레이어</p>
        </div>
        <div class="footer-links">
          <a href="./app-ads.txt" target="_blank">app-ads.txt</a>
          <a href="https://github.com/jyjy6/pitchplayer-site" target="_blank">GitHub Repository</a>
        </div>
      </div>
      <div class="footer-bottom">
        <p>© 2026 PitchPlayer. All rights reserved.</p>
      </div>
    </footer>
  </div>
</template>

<style scoped>
.page-wrapper {
  position: relative;
  z-index: 1;
  padding-bottom: 60px;
}

/* Header */
.header {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 30px 24px;
}

.logo {
  display: flex;
  align-items: center;
  gap: 12px;
  font-size: 1.5rem;
  font-weight: 800;
  letter-spacing: -0.5px;
}

.logo-icon {
  font-size: 1.8rem;
  filter: drop-shadow(0 0 10px rgba(0, 242, 254, 0.5));
}

.nav-links {
  display: flex;
  align-items: center;
  gap: 24px;
}

.nav-links a {
  color: var(--text-sub);
  text-decoration: none;
  font-weight: 600;
  transition: color 0.2s;
}

.nav-links a:hover {
  color: var(--text-main);
}

.nav-badge {
  padding: 4px 12px;
  background: rgba(0, 242, 254, 0.1);
  border: 1px solid rgba(0, 242, 254, 0.3);
  color: var(--accent-cyan) !important;
  border-radius: 999px;
  font-size: 0.85rem;
}

/* Hero */
.hero {
  padding: 60px 24px 40px;
  text-align: center;
}

.badge {
  display: inline-block;
  padding: 8px 18px;
  background: rgba(255, 255, 255, 0.05);
  border: 1px solid rgba(255, 255, 255, 0.12);
  border-radius: 999px;
  font-size: 0.9rem;
  font-weight: 600;
  color: var(--accent-cyan);
  margin-bottom: 24px;
}

.hero-title {
  font-size: 3.2rem;
  font-weight: 800;
  line-height: 1.2;
  margin-bottom: 20px;
  letter-spacing: -1px;
}

.hero-description {
  max-width: 640px;
  margin: 0 auto 36px;
  color: var(--text-sub);
  font-size: 1.15rem;
  line-height: 1.7;
}

.hero-actions {
  display: flex;
  justify-content: center;
  gap: 16px;
  margin-bottom: 50px;
  flex-wrap: wrap;
}

/* Player Mockup */
.player-mockup {
  max-width: 680px;
  margin: 0 auto;
  padding: 32px;
  text-align: left;
}

.player-header {
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin-bottom: 24px;
}

.track-info {
  display: flex;
  align-items: center;
  gap: 16px;
}

.track-album-art {
  width: 52px;
  height: 52px;
  background: linear-gradient(135deg, #1e293b, #0f172a);
  border-radius: 12px;
  display: flex;
  align-items: center;
  justify-content: center;
  font-size: 1.5rem;
  border: 1px solid rgba(255, 255, 255, 0.1);
}

.track-title {
  font-weight: 700;
  font-size: 1.1rem;
}

.track-artist {
  color: var(--text-sub);
  font-size: 0.88rem;
}

.reset-btn {
  background: rgba(255, 255, 255, 0.05);
  border: 1px solid var(--border-color);
  color: var(--text-sub);
  padding: 6px 14px;
  border-radius: 8px;
  cursor: pointer;
  font-size: 0.85rem;
  transition: all 0.2s;
}

.reset-btn:hover {
  color: var(--text-main);
  background: rgba(255, 255, 255, 0.1);
}

/* Waveform */
.waveform-container {
  height: 60px;
  background: rgba(0, 0, 0, 0.25);
  border-radius: 12px;
  padding: 10px 20px;
  margin-bottom: 28px;
  display: flex;
  align-items: center;
  border: 1px solid rgba(255, 255, 255, 0.04);
}

.waveform-bars {
  display: flex;
  align-items: center;
  justify-content: space-between;
  width: 100%;
  height: 100%;
}

.waveform-bars span {
  width: 4px;
  height: 20%;
  background: linear-gradient(180deg, var(--accent-cyan), var(--accent-purple));
  border-radius: 99px;
  transition: height 0.2s ease;
}

.waveform-bars.playing span {
  animation: wave 1s ease-in-out infinite alternate;
}

@keyframes wave {
  0% { height: 15%; }
  100% { height: 95%; }
}

/* Slider Controls */
.control-grid {
  display: flex;
  flex-direction: column;
  gap: 24px;
  margin-bottom: 28px;
}

.control-label {
  display: flex;
  justify-content: space-between;
  align-items: center;
  font-weight: 600;
  margin-bottom: 8px;
}

.control-value {
  font-weight: 700;
}

.slider {
  width: 100%;
  height: 8px;
  background: rgba(255, 255, 255, 0.1);
  border-radius: 4px;
  outline: none;
  accent-color: var(--accent-cyan);
  cursor: pointer;
}

.slider-ticks {
  display: flex;
  justify-content: space-between;
  font-size: 0.75rem;
  color: var(--text-sub);
  margin-top: 4px;
}

.player-footer {
  display: flex;
  justify-content: space-between;
  align-items: center;
  pt: 16px;
  border-top: 1px solid var(--border-color);
}

.play-btn {
  background: linear-gradient(135deg, var(--accent-cyan), var(--accent-purple));
  color: #040914;
  border: none;
  font-weight: 700;
  padding: 10px 24px;
  border-radius: 999px;
  cursor: pointer;
  transition: transform 0.2s;
}

.play-btn:hover {
  transform: scale(1.03);
}

.engine-tag {
  font-size: 0.8rem;
  color: var(--text-sub);
  background: rgba(255, 255, 255, 0.04);
  padding: 4px 10px;
  border-radius: 6px;
}

/* Features Grid */
.features-section {
  padding: 100px 24px 60px;
  text-align: center;
}

.section-title {
  font-size: 2.4rem;
  font-weight: 800;
  margin-bottom: 50px;
}

.features-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(240px, 1fr));
  gap: 24px;
}

.feature-card {
  padding: 32px 24px;
  text-align: left;
}

.feature-icon {
  font-size: 2.5rem;
  margin-bottom: 16px;
}

.feature-card h3 {
  font-size: 1.25rem;
  font-weight: 700;
  margin-bottom: 10px;
}

.feature-card p {
  color: var(--text-sub);
  font-size: 0.95rem;
  line-height: 1.6;
}

/* Footer */
.footer {
  margin-top: 80px;
  padding-top: 40px;
  border-top: 1px solid var(--border-color);
}

.footer-content {
  display: flex;
  justify-content: space-between;
  align-items: center;
  flex-wrap: wrap;
  gap: 20px;
  margin-bottom: 30px;
}

.footer-brand p {
  color: var(--text-sub);
  font-size: 0.9rem;
  margin-top: 4px;
}

.footer-links {
  display: flex;
  gap: 20px;
}

.footer-links a {
  color: var(--text-sub);
  text-decoration: none;
  font-size: 0.9rem;
}

.footer-links a:hover {
  color: var(--accent-cyan);
}

.footer-bottom {
  text-align: center;
  color: var(--text-sub);
  font-size: 0.85rem;
}

@media (max-width: 640px) {
  .hero-title {
    font-size: 2.2rem;
  }
  .player-mockup {
    padding: 20px;
  }
  .header {
    flex-direction: column;
    gap: 16px;
  }
}
</style>
