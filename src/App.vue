<script setup lang="ts">
import { computed, onMounted, onUnmounted, ref } from 'vue'

interface Hero {
  id: string
  chapter: string
  saga: string
  name: string
  alias: string
  universe: string
  narrative: string
  quote: string
  color: string
  accent: string
  image: string
  logo: string
  theme: number
  stats: { label: string; value: number }[]
}

const heroes: Hero[] = [
  {
    id: 'spider-man',
    chapter: 'CAPÍTULO I',
    saga: 'A TEIA DO DESTINO',
    name: 'Homem-Aranha',
    alias: 'Peter Parker',
    universe: 'UNIVERSO 01 · QUEENS, NY',
    narrative:
      'Mordido por uma aranha radioativa, um garoto de Queens aprendeu que toda grande força carrega uma dívida. Entre arranha-céus e becos escuros, ele balança carregando a culpa de um tio — e a esperança de uma cidade inteira.',
    quote: 'Com grandes poderes vêm grandes responsabilidades.',
    color: '#ff3b48',
    accent: '#ff8a4c',
    image: '/homem-aranha.webp',
    logo: 'spider',
    theme: 0,
    stats: [
      { label: 'Força', value: 55 },
      { label: 'Agilidade', value: 92 },
      { label: 'Inteligência', value: 84 },
    ],
  },
  {
    id: 'iron-man',
    chapter: 'CAPÍTULO II',
    saga: 'O CORAÇÃO DE FERRO',
    name: 'Homem de Ferro',
    alias: 'Tony Stark',
    universe: 'UNIVERSO 02 · MALIBU, CA',
    narrative:
      'Um bilionário egocêntrico foi sequestrado, ferido e forçado a construir sua própria sobrevivência dentro de uma caverna. Do aço nasceu um coração novo — e com ele, a responsabilidade de proteger o mundo que ele mesmo quase destruiu.',
    quote: 'Gênio, bilionário, playboy, filantropo.',
    color: '#ffb347',
    accent: '#ff5b1a',
    image: '/iron-man.jpg',
    logo: 'iron',
    theme: 1,
    stats: [
      { label: 'Força', value: 78 },
      { label: 'Tecnologia', value: 100 },
      { label: 'Carisma', value: 96 },
    ],
  },
  {
    id: 'thor',
    chapter: 'CAPÍTULO III',
    saga: 'O TROVÃO DE ASGARD',
    name: 'Thor',
    alias: 'Thor Odinson',
    universe: 'UNIVERSO 03 · ASGARD',
    narrative:
      'Exilado do próprio reino por arrogância, o Deus do Trovão aprendeu que força sem humildade é apenas ruído. Quando o Mjolnir finalmente reconheceu sua mão, o céu inteiro passou a ser seu campo de batalha.',
    quote: 'O céu inteiro é o campo de batalha.',
    color: '#ffd76a',
    accent: '#6aa8ff',
    image: '/thor.jpg',
    logo: 'thor',
    theme: 2,
    stats: [
      { label: 'Força', value: 100 },
      { label: 'Tempestade', value: 88 },
      { label: 'Dignidade', value: 95 },
    ],
  },
  {
    id: 'black-panther',
    chapter: 'CAPÍTULO IV',
    saga: 'O REI DE WAKANDA',
    name: 'Pantera Negra',
    alias: "T'Challa",
    universe: 'UNIVERSO 04 · WAKANDA',
    narrative:
      'Herdeiro de um trono milenar, T\u2019Challa carrega o peso de Wakanda nas costas. Cada passo seu é vigiado pelos ancestrais — e cada golpe, respaldado pelo vibranium que dorme sob sua nação.',
    quote: 'O traje absorve energia — e devolve com juros.',
    color: '#a78bfa',
    accent: '#5b4bff',
    image: '/pantera-negra.jpg',
    logo: 'panther',
    theme: 3,
    stats: [
      { label: 'Força', value: 82 },
      { label: 'Vibranium', value: 100 },
      { label: 'Furtividade', value: 94 },
    ],
  },
  {
    id: 'captain-america',
    chapter: 'CAPÍTULO V',
    saga: 'O SOLDADO DA ESPERANÇA',
    name: 'Capitão América',
    alias: 'Steve Rogers',
    universe: 'UNIVERSO 05 · BROOKLYN, NY',
    narrative:
      'Um garoto magrelo de Brooklyn se recusou a ficar sentado enquanto o mundo queimava. O soro o tornou forte — mas foi a coragem de se jogar sobre uma granada que o transformou em símbolo.',
    quote: 'Posso fazer isso o dia inteiro.',
    color: '#65a9ff',
    accent: '#ff4a5e',
    image: '/capitao-america.jpg',
    logo: 'captain',
    theme: 0,
    stats: [
      { label: 'Força', value: 75 },
      { label: 'Liderança', value: 98 },
      { label: 'Resistência', value: 96 },
    ],
  },
  {
    id: 'hulk',
    chapter: 'CAPÍTULO VI',
    saga: 'A FÚRIA ESMERALDA',
    name: 'Hulk',
    alias: 'Bruce Banner',
    universe: 'UNIVERSO 06 · DAYTON, OH',
    narrative:
      'A explosão de uma bomba gama dividiu um cientista em dois. De um lado, a mente brilhante de Bruce Banner. Do outro, a fúria verde que não conhece limites — e que só quer ser deixada em paz.',
    quote: 'Quanto mais irritado fica, mais forte fica.',
    color: '#6ee787',
    accent: '#3aff8c',
    image: '/hulk.jpg',
    logo: 'hulk',
    theme: 3,
    stats: [
      { label: 'Força', value: 100 },
      { label: 'Resistência', value: 100 },
      { label: 'Controle', value: 38 },
    ],
  },
  {
    id: 'doctor-strange',
    chapter: 'CAPÍTULO VII',
    saga: 'O GUARDIÃO DA REALIDADE',
    name: 'Doutor Estranho',
    alias: 'Stephen Strange',
    universe: 'UNIVERSO 07 · NOVA YORK',
    narrative:
      'Um cirurgião arrogante perdeu as mãos — e encontrou o multiverso. Entre Kamar-Taj e o Olho de Agamotto, ele aprendeu que as maiores batalhas acontecem fora do tempo.',
    quote: 'As maiores batalhas acontecem fora do tempo.',
    color: '#ff9b55',
    accent: '#ff3b48',
    image: '/doctor-strange.jpg',
    logo: 'strange',
    theme: 2,
    stats: [
      { label: 'Magia', value: 99 },
      { label: 'Conhecimento', value: 96 },
      { label: 'Estratégia', value: 92 },
    ],
  },
  {
    id: 'captain-marvel',
    chapter: 'CAPÍTULO VIII',
    saga: 'A ESTRELA CÓSMICA',
    name: 'Capitã Marvel',
    alias: 'Carol Danvers',
    universe: 'UNIVERSO 08 · ESPAÇO',
    narrative:
      'Piloto, soldado, arma. Carol Danvers foi tudo isso antes de descobrir que era muito mais. Com energia estelar correndo nas veias, ela se tornou a ponte entre a Terra e o cosmos.',
    quote: 'Uma força capaz de mudar o rumo de uma batalha.',
    color: '#ffdc73',
    accent: '#3a7bff',
    image: '/captain-marvel.jpg',
    logo: 'marvel',
    theme: 1,
    stats: [
      { label: 'Energia', value: 100 },
      { label: 'Força', value: 96 },
      { label: 'Voo', value: 94 },
    ],
  },
  {
    id: 'loki',
    chapter: 'CAPÍTULO IX',
    saga: 'O DEUS DA TRAPAÇA',
    name: 'Loki',
    alias: 'Loki Laufeyson',
    universe: 'UNIVERSO 09 · ASGARD',
    narrative:
      'Adotado, traído, traidor. O Deus da Trapaça escreveu e reescreveu sua própria história tantas vezes que nem ele sabe mais qual versão é real. Só uma coisa é certa: nunca confie na primeira impressão.',
    quote: 'Planos dentro de planos.',
    color: '#7ee6a3',
    accent: '#d4b24a',
    image: '/loki.jpg',
    logo: 'loki',
    theme: 3,
    stats: [
      { label: 'Magia', value: 94 },
      { label: 'Astúcia', value: 100 },
      { label: 'Ilusão', value: 98 },
    ],
  },
  {
    id: 'scarlet-witch',
    chapter: 'CAPÍTULO X',
    saga: 'A FEITICEIRA DO CAOS',
    name: 'Feiticeira Escarlate',
    alias: 'Wanda Maximoff',
    universe: 'UNIVERSO 10 · WESTVIEW',
    narrative:
      'Uma criança de Sokovia, um experimento da Hidra, uma feiticeira do caos. Wanda Maximoff sente a dor do mundo inteiro — e quando ela sente demais, a própria realidade se dobra.',
    quote: 'Quando seus poderes despertam, as regras mudam.',
    color: '#ff5a76',
    accent: '#c8003c',
    image: '/wanda-maximoff.jpg',
    logo: 'witch',
    theme: 2,
    stats: [
      { label: 'Magia do caos', value: 100 },
      { label: 'Telecinese', value: 97 },
      { label: 'Realidade', value: 100 },
    ],
  },
]

const ROMAN = ['I', 'II', 'III', 'IV', 'V', 'VI', 'VII', 'VIII', 'IX', 'X']

const activeIndex = ref(0)
const progress = ref(0)
const hintVisible = ref(true)

const mx = ref(0)
const my = ref(0)
let rafMouse = 0

const activeHero = computed(() => heroes[activeIndex.value])
const progressPercent = computed(() => `${progress.value * 100}%`)
const nextHero = computed(() => heroes[(activeIndex.value + 1) % heroes.length])
const position = computed(() => progress.value * (heroes.length - 1))
const activeRoman = computed(() => ROMAN[activeIndex.value] ?? String(activeIndex.value + 1))

function sceneOpacity(index: number) {
  return Math.min(
    1,
    Math.max(0, 1 - Math.abs(position.value - index) * 1.15) * 1.6,
  )
}

function sceneTransform(index: number) {
  const distance = position.value - index
  const opacity = sceneOpacity(index)
  return `translate3d(0, ${-distance * 22}px, 0) scale(${0.96 + 0.04 * opacity})`
}

function photoTransform(index: number) {
  const base = sceneTransform(index)
  const tx = mx.value * 14
  const ty = my.value * 10
  return `${base} translate3d(${tx}px, ${ty}px, 0)`
}

function onMouseMove(e: MouseEvent) {
  const x = e.clientX / window.innerWidth - 0.5
  const y = e.clientY / window.innerHeight - 0.5
  if (rafMouse) return
  rafMouse = requestAnimationFrame(() => {
    mx.value = x * 2
    my.value = y * 2
    rafMouse = 0
  })
}
function onMouseLeave() {
  mx.value = 0
  my.value = 0
}

const particles = Array.from({ length: 40 }).map(() => ({
  x: Math.random() * 100,
  y: Math.random() * 100,
  s: Math.random() * 2 + 0.6,
  d: Math.random() * 14 + 8,
  delay: Math.random() * -20,
}))

let canvas: HTMLCanvasElement | null = null
let gl: WebGLRenderingContext | null = null
let animationFrame = 0
let startTime = 0
let targetProgress = 0
let program: WebGLProgram | null = null
let uResolution: WebGLUniformLocation | null = null
let uTime: WebGLUniformLocation | null = null
let uProgress: WebGLUniformLocation | null = null

function goToHero(index: number) {
  const maxScroll =
    document.documentElement.scrollHeight - window.innerHeight
  window.scrollTo({
    top: maxScroll * (index / (heroes.length - 1)),
    behavior: 'smooth',
  })
}

function updateScroll() {
  const maxScroll =
    document.documentElement.scrollHeight - window.innerHeight
  targetProgress = maxScroll > 0 ? window.scrollY / maxScroll : 0
  hintVisible.value = targetProgress < 0.02
}

function onKey(e: KeyboardEvent) {
  if (e.key === 'ArrowDown' || e.key === 'PageDown') {
    e.preventDefault()
    goToHero(Math.min(activeIndex.value + 1, heroes.length - 1))
  } else if (e.key === 'ArrowUp' || e.key === 'PageUp') {
    e.preventDefault()
    goToHero(Math.max(activeIndex.value - 1, 0))
  }
}

function compileShader(
  context: WebGLRenderingContext,
  type: number,
  source: string,
) {
  const shader = context.createShader(type)
  if (!shader) return null
  context.shaderSource(shader, source)
  context.compileShader(shader)
  if (!context.getShaderParameter(shader, context.COMPILE_STATUS)) {
    console.error(context.getShaderInfoLog(shader))
    context.deleteShader(shader)
    return null
  }
  return shader
}

const vertexShader = `
attribute vec2 p;
void main() { gl_Position = vec4(p, 0.0, 1.0); }
`

const fragmentShader = `
precision highp float;
uniform vec2 u_res;
uniform float u_t;
uniform float u_p;

float hash(vec2 p){ return fract(sin(dot(p, vec2(127.1,311.7)))*43758.5453); }
float noise(vec2 p){
  vec2 i=floor(p); vec2 f=fract(p); f=f*f*(3.0-2.0*f);
  return mix(mix(hash(i),hash(i+vec2(1.0,0.0)),f.x),
             mix(hash(i+vec2(0.0,1.0)),hash(i+vec2(1.0,1.0)),f.x),f.y);
}
float fbm(vec2 p){
  float v=0.0, a=0.5;
  for(int i=0;i<4;i++){ v+=a*noise(p); p*=2.03; a*=0.5; }
  return v;
}
float ring(float d,float r,float t){ return 1.0-smoothstep(t*0.5,t,abs(d-r)); }
float star(vec2 uv,float s){
  vec2 p=uv*s; vec2 c=floor(p); vec2 l=fract(p)-0.5;
  float rnd=hash(c);
  float d=length(l-(vec2(hash(c+3.1),hash(c+7.7))-0.5)*0.65);
  return (1.0-smoothstep(0.015,0.04,d))*step(0.94,rnd);
}

vec3 scene(float id, vec2 uv){
  float t=u_t, d=length(uv), a=atan(uv.y,uv.x);
  float n=fbm(uv*3.0+vec2(t*0.08,-t*0.04));
  vec3 col=vec3(0.0);

  if(id<0.5){
    float spokes=abs(sin(a*10.0+0.12*sin(d*8.0)));
    float web=1.0-smoothstep(0.02,0.07,spokes*d);
    float circles=1.0-smoothstep(0.025,0.065,abs(sin(d*32.0-a*0.7)));
    col+=vec3(0.9,0.03,0.08)*web*0.7;
    col+=vec3(0.05,0.3,0.95)*circles*0.4;
  } else if(id<1.5){
    float core=exp(-d*12.0);
    float rings=ring(d,0.25,0.025)+ring(d,0.39,0.018)+ring(d,0.58,0.012);
    float circuits=1.0-smoothstep(0.015,0.05,abs(sin(uv.x*22.0+sin(uv.y*8.0)+t*0.3)));
    circuits*=step(0.25,abs(sin(uv.y*13.0)));
    col+=vec3(0.0,0.55,1.0)*core*2.0;
    col+=vec3(0.1,0.65,1.0)*rings*1.0;
    col+=vec3(1.0,0.4,0.05)*rings*0.5;
    col+=vec3(0.9,0.3,0.03)*circuits*0.25;
  } else if(id<2.5){
    float clouds=fbm(vec2(uv.x*3.0,uv.y*2.0+t*0.16));
    float bolt=abs(uv.x-0.32*sin(uv.y*8.0+t)-0.12*sin(uv.y*19.0-t*2.0));
    float lightning=(1.0-smoothstep(0.008,0.045,bolt))*step(-0.8,uv.y)*step(uv.y,0.8);
    float bolt2=abs(uv.x+0.5+0.15*sin(uv.y*12.0-t));
    lightning+=(1.0-smoothstep(0.008,0.035,bolt2))*step(-0.5,uv.y)*step(uv.y,0.55);
    col+=vec3(0.15,0.15,0.5)*clouds*1.6;
    col+=vec3(0.2,0.55,1.0)*lightning*1.8;
    col+=vec3(0.8,0.95,1.0)*lightning*lightning;
  } else if(id<3.5){
    float wave=sin(d*24.0-t*2.0+sin(a*6.0)*1.5);
    float lines=1.0-smoothstep(0.05,0.18,abs(wave));
    float claws=abs(sin(a*3.0+d*5.0));
    col+=vec3(0.35,0.05,0.9)*lines*0.9;
    col+=vec3(0.05,0.35,0.9)*(1.0-smoothstep(0.0,0.04,claws))*0.55;
  } else if(id<4.5){
    float rings=ring(d,0.28,0.055)+ring(d,0.48,0.055)+ring(d,0.68,0.055);
    float center=exp(-d*9.0);
    float stars=star(uv+vec2(0.0,t*0.025),18.0);
    col+=vec3(0.8,0.05,0.08)*rings*1.0;
    col+=vec3(0.05,0.3,0.9)*rings*0.5;
    col+=vec3(0.9,0.95,1.0)*center*0.7;
    col+=vec3(0.9,0.95,1.0)*stars*0.9;
  } else if(id<5.5){
    float energy=fbm(uv*4.0+vec2(t*0.12,-t*0.2));
    float veins=abs(sin(uv.x*12.0+sin(uv.y*8.0+t)*2.0));
    col+=vec3(0.03,0.4,0.1)*energy*2.2;
    col+=vec3(0.15,1.0,0.2)*(1.0-smoothstep(0.0,0.12,veins))*0.35;
  } else if(id<6.5){
    float portal=ring(d,0.4,0.025)+ring(d,0.48,0.018)+ring(d,0.57,0.012);
    float glyphs=abs(sin(a*18.0+sin(d*16.0)+t*0.8));
    float magic=(1.0-smoothstep(0.05,0.22,glyphs))*smoothstep(0.2,0.35,d)*(1.0-smoothstep(0.62,0.8,d));
    col+=vec3(1.0,0.3,0.03)*portal*1.2;
    col+=vec3(1.0,0.55,0.05)*magic*0.7;
  } else if(id<7.5){
    float rays=pow(abs(cos(a*9.0+t*0.25)),12.0);
    float burst=exp(-d*2.2);
    float stars=star(uv+vec2(t*0.02,0.0),24.0);
    col+=vec3(0.1,0.3,1.0)*rays*1.0;
    col+=vec3(1.0,0.4,0.05)*burst*0.9;
    col+=vec3(1.0,0.8,0.25)*stars*1.2;
  } else if(id<8.5){
    float spiral=sin(a*5.0+d*13.0-t*0.7);
    float ribbons=1.0-smoothstep(0.03,0.15,abs(spiral));
    float geometry=abs(sin(a*6.0+d*4.0));
    col+=vec3(0.05,0.6,0.2)*ribbons*1.0;
    col+=vec3(1.0,0.6,0.08)*(1.0-smoothstep(0.0,0.08,geometry))*0.55;
  } else {
    float chaos=fbm(uv*5.0+vec2(t*0.1,-t*0.14));
    float waves=sin(a*7.0+d*18.0-t*1.2);
    float magic=1.0-smoothstep(0.0,0.18,abs(waves));
    col+=vec3(0.8,0.02,0.12)*chaos*1.7;
    col+=vec3(1.0,0.05,0.2)*magic*0.75;
  }

  float vig=1.0-smoothstep(0.35,1.35,d);
  col*=0.35+vig*0.9;
  return col;
}

void main(){
  vec2 uv=(gl_FragCoord.xy-0.5*u_res)/u_res.y;
  float p=clamp(u_p,0.0,1.0)*9.0;
  float cur=floor(p);
  float nxt=min(cur+1.0,9.0);
  float blend=smoothstep(0.12,0.88,fract(p));
  vec3 c=mix(scene(cur,uv),scene(nxt,uv),blend);
  gl_FragColor=vec4(c,1.0);
}
`

function resizeCanvas() {
  if (!canvas || !gl) return
  const dpr = Math.min(window.devicePixelRatio || 1, 1.5) * 0.75
  const w = Math.floor(canvas.clientWidth * dpr)
  const h = Math.floor(canvas.clientHeight * dpr)
  if (canvas.width !== w || canvas.height !== h) {
    canvas.width = w
    canvas.height = h
    gl.viewport(0, 0, w, h)
  }
}

function render(now: number) {
  resizeCanvas()
  progress.value += (targetProgress - progress.value) * 0.1
  if (Math.abs(targetProgress - progress.value) < 0.0005)
    progress.value = targetProgress
  activeIndex.value = Math.min(
    Math.round(progress.value * (heroes.length - 1)),
    heroes.length - 1,
  )
  if (gl && program) {
    gl.useProgram(program)
    gl.uniform2f(uResolution, canvas!.width, canvas!.height)
    gl.uniform1f(uTime, (now - startTime) / 1000)
    gl.uniform1f(uProgress, progress.value)
    gl.drawArrays(gl.TRIANGLES, 0, 3)
  }
  animationFrame = requestAnimationFrame(render)
}

onMounted(() => {
  canvas = document.querySelector('#gl')
  gl = canvas?.getContext('webgl', { antialias: false, alpha: true }) ?? null

  if (gl) {
    const vs = compileShader(gl, gl.VERTEX_SHADER, vertexShader)
    const fs = compileShader(gl, gl.FRAGMENT_SHADER, fragmentShader)
    if (vs && fs) {
      program = gl.createProgram()
      if (program) {
        gl.attachShader(program, vs)
        gl.attachShader(program, fs)
        gl.linkProgram(program)
        if (gl.getProgramParameter(program, gl.LINK_STATUS)) {
          gl.useProgram(program)
          const buffer = gl.createBuffer()
          gl.bindBuffer(gl.ARRAY_BUFFER, buffer)
          gl.bufferData(
            gl.ARRAY_BUFFER,
            new Float32Array([-1, -1, 3, -1, -1, 3]),
            gl.STATIC_DRAW,
          )
          const loc = gl.getAttribLocation(program, 'p')
          gl.enableVertexAttribArray(loc)
          gl.vertexAttribPointer(loc, 2, gl.FLOAT, false, 0, 0)
          uResolution = gl.getUniformLocation(program, 'u_res')
          uTime = gl.getUniformLocation(program, 'u_t')
          uProgress = gl.getUniformLocation(program, 'u_p')
        } else {
          program = null
          gl = null
        }
      }
    }
  }

  window.addEventListener('scroll', updateScroll, { passive: true })
  window.addEventListener('resize', resizeCanvas)
  window.addEventListener('keydown', onKey)
  updateScroll()
  resizeCanvas()
  startTime = performance.now()
  animationFrame = requestAnimationFrame(render)
})

onUnmounted(() => {
  window.removeEventListener('scroll', updateScroll)
  window.removeEventListener('resize', resizeCanvas)
  window.removeEventListener('keydown', onKey)
  cancelAnimationFrame(animationFrame)
  if (rafMouse) cancelAnimationFrame(rafMouse)
})
</script>

<template>
  <main @mousemove="onMouseMove" @mouseleave="onMouseLeave">
    <!-- CAMADA 0: fotos com Ken Burns + paralaxe -->
    <div class="photo-stage" aria-hidden="true">
      <div
        v-for="(hero, i) in heroes"
        :key="hero.id"
        class="photo"
        :style="{
          opacity: sceneOpacity(i) * 0.85,
          transform: photoTransform(i),
          '--c': hero.color,
          '--a': hero.accent,
        }"
      >
        <img :src="hero.image" :alt="hero.name" loading="lazy" />
      </div>
    </div>

    <!-- CAMADA 1: color grade -->
    <div class="grade grade-mult" :style="{ '--c': activeHero.color }" aria-hidden="true"></div>
    <div class="grade grade-screen" :style="{ '--c': activeHero.accent }" aria-hidden="true"></div>

    <!-- CAMADA 2: WebGL -->
    <canvas id="gl" aria-hidden="true"></canvas>

    <!-- CAMADA 3: poeira -->
    <div class="dust" aria-hidden="true">
      <span
        v-for="(p, i) in particles"
        :key="i"
        :style="{
          left: p.x + '%',
          top: p.y + '%',
          width: p.s + 'px',
          height: p.s + 'px',
          animationDuration: p.d + 's',
          animationDelay: p.delay + 's',
          '--c': activeHero.color,
        }"
      ></span>
    </div>

    <!-- CAMADA 4: marca editorial do capítulo -->
    <div class="chapter-mark" aria-hidden="true">
      <span
        :key="activeHero.id + '-roman'"
        class="roman"
        :style="{ '--c': activeHero.color, '--a': activeHero.accent }"
      >{{ activeRoman }}</span>
    </div>

    <!-- CAMADA 5: name rail vertical -->
    <div class="name-rail" :style="{ '--c': activeHero.color }" aria-hidden="true">
      <span class="rline"></span>
      <span :key="activeHero.id + '-rail'" class="rname">{{ activeHero.name }}</span>
      <span class="rline"></span>
    </div>

    <!-- HUD -->
    <div class="progress"><i :style="{ width: progressPercent }"></i></div>

    <header class="hud">
      <div class="brand"><b>MARVEL</b> // MULTIVERSO</div>
      <div class="idx">
        {{ String(activeIndex + 1).padStart(2, '0') }}
        <span>/</span>
        {{ String(heroes.length).padStart(2, '0') }}
      </div>
    </header>

    <nav class="nav" aria-label="Navegação dos heróis">
      <button
        v-for="(hero, index) in heroes"
        :key="hero.id"
        :class="{ on: activeIndex === index }"
        :aria-label="hero.name"
        :title="hero.name"
        :style="{ '--dot-color': hero.color }"
        @click="goToHero(index)"
      ></button>
    </nav>

    <div class="hint" :class="{ hidden: !hintVisible }">
      Role para atravessar o multiverso
      <span>↓</span>
    </div>

    <!-- CAMADA 6: track de texto -->
    <div class="track" :style="{ height: `${heroes.length * 100}vh` }">
      <section v-for="(hero, index) in heroes" :key="hero.id" class="scene">
        <div
          class="scene-content"
          :class="{ active: activeIndex === index }"
          :style="{
            opacity: sceneOpacity(index),
            transform: sceneTransform(index),
            '--hero-color': hero.color,
          }"
        >
          <div class="copy">
            <div class="ktag">
              <span class="dot"></span>
              {{ hero.universe }}
            </div>
            <div class="chap">
              <span class="num">{{ hero.chapter }}</span>
              <span class="saga">— {{ hero.saga }}</span>
            </div>
            <p class="alias">{{ hero.alias }}</p>
            <h1 class="name">{{ hero.name }}</h1>
            <p class="narrative">{{ hero.narrative }}</p>
            <blockquote class="quote">“{{ hero.quote }}”</blockquote>

            <div class="stats">
              <div v-for="stat in hero.stats" :key="stat.label" class="stat">
                <div class="lbl">{{ stat.label }}</div>
                <div class="bar"><i :style="{ width: `${stat.value}%` }"></i></div>
                <div class="val">{{ stat.value }}</div>
              </div>
            </div>

            <button class="cta" @click="goToHero((index + 1) % heroes.length)">
              Atravessar o próximo portal
              <span aria-hidden="true">→</span>
            </button>

            <div class="next-teaser" :style="{ '--next-color': nextHero.color }">
              <span class="teaser-label">A seguir</span>
              <span class="teaser-name">{{ nextHero.name }}</span>
            </div>
          </div>
        </div>
      </section>
    </div>
  </main>
</template>

<style>
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

html {
  scroll-behavior: smooth;
  background: #05070f;
}

body {
  min-width: 320px;
  overflow-x: hidden;
  background: #05070f;
  color: #fff;
  font-family: "Inter", "Segoe UI", system-ui, -apple-system, sans-serif;
  -webkit-font-smoothing: antialiased;
}

button { font: inherit; }
#app, main { min-height: 100vh; }

.photo-stage {
  position: fixed;
  inset: 0;
  z-index: 0;
  overflow: hidden;
}
.photo {
  position: absolute;
  inset: -3%;
  will-change: opacity, transform;
  transition: opacity 0.6s ease;
}
.photo img {
  width: 100%;
  height: 100%;
  object-fit: cover;
  display: block;
  opacity: 0.62;
  filter: contrast(1.18) brightness(0.55) saturate(0.25);
  animation: kenburns 26s ease-in-out infinite alternate;
  will-change: transform;
}
@keyframes kenburns {
  0% {
    transform: scale(1.05) translate(0%, 0%);
  }
  100% {
    transform: scale(1.18) translate(-2.5%, -1.8%);
  }
}
.photo::after {
  content: '';
  position: absolute;
  inset: 0;
  background:
    radial-gradient(
      ellipse at 62% 55%,
      color-mix(in srgb, var(--c) 45%, transparent) 0%,
      transparent 60%
    ),
    radial-gradient(
      ellipse at 20% 90%,
      color-mix(in srgb, var(--a) 30%, transparent) 0%,
      transparent 55%
    );
  mix-blend-mode: screen;
}

.grade {
  position: fixed;
  inset: 0;
  z-index: 1;
  pointer-events: none;
}
.grade-mult {
  background: var(--c);
  mix-blend-mode: color;
  opacity: 0.55;
  transition: background 0.6s ease;
}
.grade-screen {
  background: radial-gradient(
    ellipse at 60% 40%,
    color-mix(in srgb, var(--c) 20%, transparent),
    transparent 70%
  );
  mix-blend-mode: screen;
  opacity: 0.75;
  transition: background 0.6s ease;
}

#gl {
  position: fixed;
  inset: 0;
  width: 100%;
  height: 100%;
  display: block;
  z-index: 2;
  mix-blend-mode: screen;
  opacity: 0.7;
  pointer-events: none;
}

.dust {
  position: fixed;
  inset: 0;
  z-index: 3;
  pointer-events: none;
  overflow: hidden;
}
.dust span {
  position: absolute;
  display: block;
  border-radius: 50%;
  background: var(--c, #fff);
  box-shadow: 0 0 10px var(--c, #fff);
  opacity: 0;
  animation: float linear infinite;
}
@keyframes float {
  0%   { transform: translateY(0) scale(0.4); opacity: 0; }
  15%  { opacity: 0.9; }
  85%  { opacity: 0.6; }
  100% { transform: translateY(-110vh) scale(1.2); opacity: 0; }
}

.chapter-mark {
  position: fixed;
  top: 50%;
  right: -3vw;
  transform: translateY(-50%);
  z-index: 4;
  pointer-events: none;
  user-select: none;
  overflow: hidden;
  max-width: 60vw;
}
.chapter-mark .roman {
  display: block;
  font-family: "Times New Roman", "Playfair Display", serif;
  font-weight: 900;
  font-size: clamp(200px, 32vw, 520px);
  line-height: 0.82;
  letter-spacing: -0.04em;
  color: transparent;
  -webkit-text-stroke: 1.5px color-mix(in srgb, var(--c) 45%, transparent);
  text-shadow:
    0 0 60px color-mix(in srgb, var(--c) 30%, transparent),
    0 0 120px color-mix(in srgb, var(--a) 20%, transparent);
  opacity: 0.55;
  animation: romanEnter 0.9s cubic-bezier(0.2, 0.9, 0.15, 1);
  will-change: transform, opacity;
}
@keyframes romanEnter {
  0% {
    opacity: 0;
    transform: translateX(50px) scale(0.94);
    filter: blur(14px);
  }
  100% {
    opacity: 0.55;
    transform: translateX(0) scale(1);
    filter: blur(0);
  }
}

.name-rail {
  position: fixed;
  right: 22px;
  top: 50%;
  transform: translateY(-50%);
  z-index: 5;
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 20px;
  pointer-events: none;
  color: var(--c);
}
.name-rail .rline {
  width: 1px;
  height: 90px;
  background: linear-gradient(
    180deg,
    transparent,
    color-mix(in srgb, var(--c) 55%, transparent),
    transparent
  );
}
.name-rail .rname {
  writing-mode: vertical-rl;
  transform: rotate(180deg);
  font-size: 11px;
  letter-spacing: 6px;
  text-transform: uppercase;
  font-weight: 700;
  color: color-mix(in srgb, var(--c) 90%, #fff);
  text-shadow: 0 0 18px color-mix(in srgb, var(--c) 60%, transparent);
  animation: railEnter 0.8s cubic-bezier(0.2, 0.9, 0.15, 1);
  white-space: nowrap;
}
@keyframes railEnter {
  0% {
    opacity: 0;
    transform: rotate(180deg) translateY(-12px);
    filter: blur(6px);
  }
  100% {
    opacity: 1;
    transform: rotate(180deg) translateY(0);
    filter: blur(0);
  }
}

.progress {
  position: fixed;
  top: 0;
  left: 0;
  right: 0;
  height: 3px;
  z-index: 30;
  background: rgba(255, 255, 255, 0.06);
}
.progress i {
  display: block;
  height: 100%;
  background: linear-gradient(90deg, #ff5a5e, #ffb347, #6ee787, #65a9ff, #a78bfa, #ff5a76);
  box-shadow: 0 0 14px rgba(255, 255, 255, 0.5);
  transition: width 0.15s linear;
}

.hud {
  position: fixed;
  top: 20px;
  left: 0;
  right: 0;
  display: flex;
  justify-content: space-between;
  padding: 0 28px;
  z-index: 30;
  pointer-events: none;
  font-size: 13px;
  letter-spacing: 3px;
  color: #ffffffb8;
}
.hud b { color: #fff; font-weight: 800; }
.idx {
  font-variant-numeric: tabular-nums;
  color: #fff;
  font-weight: 600;
}
.idx span { opacity: 0.4; margin: 0 2px; }

.nav {
  position: fixed;
  left: 24px;
  top: 50%;
  transform: translateY(-50%);
  display: flex;
  flex-direction: column;
  gap: 12px;
  z-index: 30;
}
.nav button {
  width: 10px;
  height: 10px;
  border-radius: 50%;
  border: 1.5px solid #ffffff8c;
  background: transparent;
  cursor: pointer;
  transition: all 0.25s ease;
  padding: 0;
}
.nav button:hover { border-color: #fff; transform: scale(1.2); }
.nav button.on {
  background: var(--dot-color, #fff);
  border-color: var(--dot-color, #fff);
  transform: scale(1.5);
  box-shadow: 0 0 14px var(--dot-color, #fff);
}

.hint {
  position: fixed;
  bottom: 22px;
  left: 50%;
  transform: translateX(-50%);
  z-index: 30;
  display: flex;
  gap: 8px;
  align-items: center;
  color: #ffffffb3;
  font-size: 12px;
  letter-spacing: 2px;
  white-space: nowrap;
  transition: opacity 0.35s;
  animation: bob 1.6s ease-in-out infinite;
  pointer-events: none;
  text-transform: uppercase;
}
.hint.hidden { opacity: 0; }
@keyframes bob {
  0%, 100% { transform: translate(-50%, 0); }
  50% { transform: translate(-50%, 7px); }
}

.track {
  position: relative;
  z-index: 10;
}
.scene {
  position: relative;
  height: 100vh;
}
.scene-content {
  position: fixed;
  inset: 0;
  z-index: 5;
  display: flex;
  flex-direction: column;
  justify-content: flex-end;
  padding: 0 6vw 9vh;
  pointer-events: none;
  will-change: opacity, transform;
}
.scene-content.active { pointer-events: auto; }

.copy { max-width: min(620px, 46vw); }

.copy > * {
  opacity: 0;
  transform: translateY(22px);
  filter: blur(6px);
  transition:
    opacity 0.7s cubic-bezier(0.2, 0.9, 0.15, 1),
    transform 0.7s cubic-bezier(0.2, 0.9, 0.15, 1),
    filter 0.7s cubic-bezier(0.2, 0.9, 0.15, 1);
}
.scene-content.active .copy > * {
  opacity: 1;
  transform: translateY(0);
  filter: blur(0);
}
.scene-content.active .copy > *:nth-child(1)  { transition-delay: 0.05s; }
.scene-content.active .copy > *:nth-child(2)  { transition-delay: 0.12s; }
.scene-content.active .copy > *:nth-child(3)  { transition-delay: 0.18s; }
.scene-content.active .copy > *:nth-child(4)  { transition-delay: 0.24s; }
.scene-content.active .copy > *:nth-child(5)  { transition-delay: 0.32s; }
.scene-content.active .copy > *:nth-child(6)  { transition-delay: 0.40s; }
.scene-content.active .copy > *:nth-child(7)  { transition-delay: 0.48s; }
.scene-content.active .copy > *:nth-child(8)  { transition-delay: 0.56s; }
.scene-content.active .copy > *:nth-child(9)  { transition-delay: 0.64s; }

.ktag {
  display: flex;
  align-items: center;
  gap: 10px;
  color: var(--hero-color);
  font-size: 12px;
  letter-spacing: 3px;
  margin-bottom: 14px;
  font-weight: 600;
}
.dot {
  width: 7px;
  height: 7px;
  border-radius: 50%;
  background: currentColor;
  box-shadow: 0 0 10px currentColor;
  animation: pulse 1.8s ease-in-out infinite;
}
@keyframes pulse {
  0%, 100% { transform: scale(1); opacity: 1; }
  50% { transform: scale(1.4); opacity: 0.6; }
}
.chap {
  display: flex;
  align-items: baseline;
  gap: 12px;
  margin-bottom: 18px;
  font-size: 12px;
  letter-spacing: 3px;
  text-transform: uppercase;
}
.chap .num { color: #fff; font-weight: 700; }
.chap .saga { color: var(--hero-color); font-weight: 600; }

.alias {
  font-size: 12px;
  color: #ffffff8c;
  letter-spacing: 4px;
  text-transform: uppercase;
  margin-bottom: 6px;
}
.name {
  margin-bottom: 18px;
  font-size: clamp(42px, 7vw, 92px);
  font-weight: 800;
  line-height: 0.98;
  letter-spacing: -0.03em;
  text-shadow: 0 4px 50px rgba(0, 0, 0, 0.85);
  background: linear-gradient(
    180deg,
    #fff 0%,
    #fff 55%,
    color-mix(in srgb, var(--hero-color) 60%, #fff) 100%
  );
  -webkit-background-clip: text;
  background-clip: text;
  -webkit-text-fill-color: transparent;
}
.narrative {
  max-width: 520px;
  margin-bottom: 16px;
  font-size: clamp(13px, 1vw, 15px);
  line-height: 1.7;
  color: #ffffffc4;
}
.quote {
  max-width: 520px;
  margin-bottom: 24px;
  padding-left: 14px;
  border-left: 2px solid var(--hero-color);
  font-size: clamp(12px, 0.9vw, 14px);
  line-height: 1.6;
  font-style: italic;
  color: #ffffff9c;
}
.stats {
  display: flex;
  flex-wrap: wrap;
  gap: 22px;
}
.stat { min-width: 104px; max-width: 160px; }
.lbl {
  font-size: 11px;
  letter-spacing: 1.5px;
  text-transform: uppercase;
  color: #ffffff99;
}
.bar {
  height: 4px;
  margin: 8px 0 6px;
  overflow: hidden;
  border-radius: 2px;
  background: #ffffff24;
}
.bar i {
  display: block;
  height: 100%;
  border-radius: 2px;
  background: var(--hero-color);
  box-shadow: 0 0 10px var(--hero-color);
  transition: width 0.8s cubic-bezier(0.4, 0, 0.2, 1);
}
.val {
  font-size: 13px;
  font-variant-numeric: tabular-nums;
  color: #ffffffcc;
}

.cta {
  display: inline-flex;
  align-items: center;
  align-self: flex-start;
  gap: 10px;
  margin-top: 26px;
  padding: 13px 24px;
  border: 1px solid color-mix(in srgb, var(--hero-color) 60%, transparent);
  border-radius: 999px;
  background: color-mix(in srgb, var(--hero-color) 12%, transparent);
  color: #fff;
  font-size: 12px;
  letter-spacing: 2px;
  text-transform: uppercase;
  font-weight: 600;
  cursor: pointer;
  transition: all 0.28s ease;
  backdrop-filter: blur(8px);
}
.cta:hover {
  background: color-mix(in srgb, var(--hero-color) 30%, transparent);
  border-color: var(--hero-color);
  transform: translateY(-2px);
  box-shadow: 0 8px 30px color-mix(in srgb, var(--hero-color) 40%, transparent);
}
.cta span { transition: transform 0.28s ease; }
.cta:hover span { transform: translateX(4px); }

.next-teaser {
  display: flex;
  align-items: center;
  gap: 10px;
  margin-top: 18px;
  font-size: 11px;
  letter-spacing: 2px;
  text-transform: uppercase;
}
.teaser-label { color: #ffffff66; }
.teaser-name { color: var(--next-color); font-weight: 700; }

@media (max-width: 900px) {
  .copy { max-width: 100%; }

  .chapter-mark {
    top: 8vh;
    right: -6vw;
    transform: none;
    max-width: 90vw;
  }
  .chapter-mark .roman {
    font-size: clamp(140px, 34vw, 260px);
    opacity: 0.35;
  }

  .name-rail {
    right: 10px;
    gap: 12px;
  }
  .name-rail .rname { font-size: 10px; letter-spacing: 4px; }
  .name-rail .rline { height: 60px; }

  .nav {
    left: auto;
    right: 14px;
  }

  .scene-content {
    padding: 0 7vw 8vh;
    background: linear-gradient(180deg, transparent 0%, transparent 38%, rgba(5, 7, 15, 0.9) 100%);
  }
}

@media (max-width: 640px) {
  .hud { padding: 0 16px; font-size: 10px; letter-spacing: 1.5px; }
  .nav { right: 10px; gap: 10px; }
  .nav button { width: 8px; height: 8px; }
  .name-rail { display: none; }
  .scene-content { padding: 0 6vw 7vh; }
  .ktag { font-size: 10px; letter-spacing: 1.5px; margin-bottom: 10px; }
  .chap { font-size: 10px; letter-spacing: 1.5px; margin-bottom: 12px; }
  .name { font-size: clamp(34px, 11vw, 56px); margin-bottom: 12px; }
  .narrative { font-size: 12.5px; line-height: 1.6; margin-bottom: 12px; max-width: 100%; }
  .quote { font-size: 11.5px; margin-bottom: 16px; }
  .stats { gap: 12px; }
  .stat { min-width: 74px; max-width: 27vw; }
  .lbl { font-size: 9px; letter-spacing: 0.8px; }
  .val { font-size: 11px; }
  .cta { margin-top: 20px; padding: 11px 16px; font-size: 10px; letter-spacing: 1.5px; }
  .next-teaser { font-size: 9px; margin-top: 12px; }
  .hint { bottom: 12px; font-size: 10px; }
  .chapter-mark .roman { opacity: 0.28; }
}

@media (prefers-reduced-motion: reduce) {
  html { scroll-behavior: auto; }
  *, *::before, *::after {
    animation-duration: 0.01ms !important;
    transition-duration: 0.01ms !important;
  }
}
</style>