<template>
  <div id="app">
    <img alt="Echoes from Silence" src="./assets/logoEFS.png" class="logo" />
    <section v-for="(section, idx) in sections" :key="idx" :ref="'section' + idx"
      :class="['fade-section', { visible: visibleSections[idx] }]">
      <img v-if="section.image" :src="section.image" :alt="section.title" class="section-image" />
      <h2 v-if="section.title">{{ section.title }}</h2>
      <p v-if="section.content">{{ section.content }}</p>
      <div v-if="section.members" class="members-section">
        <div v-for="(member, memberIdx) in section.members" :key="member.name" 
             :ref="'member' + idx + '_' + memberIdx"
             :class="['member', { visible: visibleMembers[idx + '_' + memberIdx] }]">
          <img :src="member.image" :alt="member.name" class="member-image" />
          <h3>{{ member.name }}</h3>
          <p>{{ member.description }}</p>
        </div>
      </div>
    </section>
    <button v-if="showScrollTop" class="scroll-top-btn" @click="scrollToTop" aria-label="Volver arriba">
      ↑
    </button>
  </div>
</template>

<script>
export default {
  name: 'App',
  data() {
    return {
      sections: [
        {
          image: require('./assets/efs-horizontal1.jpg')
        },
        {
          title: 'Sobre Nosotros',
          content: 'Formada en 2020, Echoes fusiona rock, pop y electrónica en cada presentación.',
          members: [
            {
              name: 'Carlos',
              image: require('./assets/carlos.jpg'),
              description: 'Carlos es uno de los encargados de dar guitarrazos y poner su voz a los coros de Echoes from Silence, además de ser el técnico de sonido y productor del grupo, el chico orquesta, vamos…¡! Su pasión por la música y sobretodo por la guitarra, hace que lleve tocando este instrumento desde hace catorce años de manera autodidacta. Con este grupo buscaba hacer algo diferente a los otros proyectos que tuvo anteriormente: Weed Out (guitarrista y cantante), Q11 (bajista), Sistema Kadaver (guitarrista y corista), Trumpeters (guitarrista) y Mientras Llueve (guitarrista y cantante). Sus influencias abarcan desde el flamenco fusión hasta el metal extremo, como Canteca de Macao, Héroes del Silencio, Extremoduro, Envidia Kotxina, Iron Maiden, Linkin Park, Within Temptation, Slipknot, While She Sleeps, Korn, Jinjer o Infant Annihilator.'
            },
            {
              name: 'Dani',
              image: require('./assets/dani.jpg'),
              description: 'Dani es uno de los guitarristas de la formación. Amante de las seis cuerdas que se dedica, al menos una vez al día, a pasar tiempo con sus "queridas". Empezó tocando a los doce años con otros dos amigos. Avanzaron y mejoraron musicalmente juntos, cada uno en su propio estilo. Creció tocando con colegas para colegas, haciendo covers con una peculiar versión hilarante de la letra… momentos de diversión en familia. Cuando surgió la idea de una formación seria, ni se lo pensó dos veces… "¡Joder, pues claro que si!". Anteriormente formó parte de otro proyecto musical, Umbilical A.L.I.V.E. Tiene gustos musicales de todos los colores, pero lo que de verdad le pone eufórico es el thrash metal. Entre sus influencias destacan: Pantera, Audioslave, Megadeth, Annihilator, Gojira, Alice in Chains, Tool, Kreator, Faith No More, Blind Guardian, Anthrax, Rage, BLS...'
            },
            {
              name: 'Diego',
              image: require('./assets/diego.jpg'),
              description: 'Diego (Yisus) es el encargado de desatar el rugido de los tambores. Empezó hace catorce años golpeando cacerolas de manera autodidacta, hasta poder estrenar una batería de verdad con su primer grupo de rock and roll (Ladrillo), mientras pasaba el tiempo fue enlazando proyectos diferentes abarcando rock (Q11), Ska-Punk (Sistema Kadaver) o géneros sin identificar (The Trumpeters). Pasado el tiempo y tras una junta apocalíptica, emergió la idea de este proyecto y ya no había marcha atrás…. ¡¡Preparad vuestros tímpanos!! "TUCUPÁ TUCUPÁ". Entre sus influencias destacan: Slipknot, System Of A Down, Los De Marras, Eskimo Callboy, Skindred, Narco, Extremoduro, Ofunkillo, Iratxo, Koma, Korpiklaani...'
            },
            {
              name: 'María',
              image: require('./assets/maria.jpg'),
              description: 'María es nuestra bajista, encargada de hacer que nos tiemble el pecho. Es también nuestra integrante más joven y por ello nos hace ver las cosas desde otra perspectiva. Comenzó tocando el ukelele hace cinco años y un año después empezó como bajista en su primer proyecto, La Caída, de género rock, hasta que Carlos la secuestró y se la llevó al que sería su siguiente proyecto, Mientras Llueve, con un estilo más acorde a sus gustos musicales, donde fue perfeccionando su técnica y definiendo su estilo.En este proyecto, Echoes from Silence, sigue reinventándose y experimentando musicalmente.Entre sus influencias destacan: Slipknot, Bring Me The Horizon, Bullet For My Valentine, System Of A Down, Korn, Incubus, Limp Bizkit, Gojira, Ill Niño, Static X, Papa Roach, Billy Talent, Killswitch Engage o Trivium.'
            },
            {
              name: 'Raquel',
              image: require('./assets/raquel.jpg'),
              description: 'Os presentamos a Raquel, nuestra vocalista principal. Ella más de ocho años cantando en coros de música clásica como soprano, empezando por la Coral Universitaria de Murcia, el Coro Joven de Murcia, entre otros proyectos corales y actualmente canta en el Coro Diatessaron. Desde hacía tiempo tenía ilusión por tener un grupo y explorar otros géneros. En Echoes from Silence, ha descubierto que del barroco se sale, que puede cantar cosas más modernas. Es un género que le encanta, del que está aprendiendo mucho y le está ayudando a explorar su voz. Sus gustos musicales son muy diversos, desde Bach, pasando por Zahara, Mónica Naranjo hasta Epica, Within Temptation, Xandria, Trees of Eternity, God is an astronaut, Anathema…'
            },
            {
              name: 'Vanesa',
              image: require('./assets/vanesa.jpg'),
              description: 'Vanesa es la encargada de dar vida a los teclados y coros de Echoes from Silence. De pequeña, soñaba con tener un grupo en el que tocar la guitarra y cantar al ritmo de unos buenos riffs. Estudió dos años de guitarra española pero como lo suyo era la eléctrica y no conocía a nadie para aprender, lo dejó para dedicarse a otro instrumento que le despertaba curiosidad, el piano. Estudió cuatro años en la Escuela de Música de su pueblo pero como no le iba el clásico, lo volvió a dejar para aprender de manera autodidacta tocando lo que le gustaba. Este es el primer proyecto serio del que forma parte. Entre sus influencias hay grupos muy variados como Queen, Ratt, KISS, The Cranberries, Dover, Evanescence, Arch Enemy, Amorphis o Avatar.'
            }
          ]
        },
        {
          title: 'Música',
          content: 'Escucha nuestros últimos lanzamientos en Spotify, Apple Music y más.',
        },
        {
          title: 'Próximos Conciertos',
          content: 'Consulta nuestras fechas y acompáñanos en vivo.',
        },
        {
          title: 'Contacto',
          content: '¿Quieres contratarnos o colaborar? ¡Escríbenos!',
        },
      ],
      visibleSections: [],
      visibleMembers: {},
      showScrollTop: false,
    };
  },
  mounted() {
    this.visibleSections = this.sections.map(() => false);
    window.addEventListener('scroll', this.handleScroll);
    this.handleScroll();
  },
  beforeUnmount() {
    window.removeEventListener('scroll', this.handleScroll);
  },
  methods: {
    handleScroll() {
      this.sections.forEach((section, idx) => {
        let el = this.$refs['section' + idx];
        if (Array.isArray(el)) {
          el = el[0];
        }
        if (el && typeof el.getBoundingClientRect === 'function') {
          const rect = el.getBoundingClientRect();
          if (rect.top < window.innerHeight * 0.8) {
            this.visibleSections[idx] = true;
          }
        }

        // Handle member visibility
        if (section.members) {
          section.members.forEach((_, memberIdx) => {
            const memberKey = idx + '_' + memberIdx;
            let memberEl = this.$refs['member' + memberKey];
            if (Array.isArray(memberEl)) {
              memberEl = memberEl[0];
            }
            if (memberEl && typeof memberEl.getBoundingClientRect === 'function') {
              const memberRect = memberEl.getBoundingClientRect();
              if (memberRect.top < window.innerHeight * 0.9) {
                this.visibleMembers[memberKey] = true;
              }
            }
          });
        }
      });
      this.showScrollTop = window.scrollY > 200;
    },
    scrollToTop() {
      window.scrollTo({ top: 0, behavior: 'smooth' });
    },
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  text-align: center;
  color: #2c3e50;
  background-color: rgba(0, 0, 0, 0.914);
  min-height: 100vh;
  padding-bottom: 40px;
  display: flex;
  flex-direction: column;
  align-items: center;
}

.logo {
  max-width: 40%;
  height: auto;
  filter: invert(1);
  margin: 40px 0 20px 0;
}

.fade-section {
  opacity: 0;
  transform: translateY(40px);
  transition: opacity 0.8s, transform 0.8s;
  max-width: 800px;
  width: 90%;
  margin: 20px auto;
  background: rgba(255, 255, 255, 0.07);
  border-radius: 16px;
  padding: 32px 24px;
  box-shadow: 0 4px 24px rgba(0, 0, 0, 0.2);
}

.fade-section.visible {
  opacity: 1;
  transform: translateY(0);
}

h2 {
  margin-bottom: 16px;
  color: #e0e0e0;
}

p {
  color: #c0c0c0;
  font-size: 1.1em;
}

.scroll-top-btn {
  position: fixed;
  right: 32px;
  bottom: 32px;
  background: #222;
  color: #fff;
  border: none;
  border-radius: 50%;
  width: 48px;
  height: 48px;
  font-size: 2em;
  cursor: pointer;
  box-shadow: 0 2px 8px rgba(0, 0, 0, 0.3);
  opacity: 0.8;
  transition: opacity 0.2s;
  z-index: 1000;
}

.scroll-top-btn:hover {
  opacity: 1;
}

.section-image {
  max-width: 100%;
  height: auto;
  display: block;
  margin: 0 auto 20px auto;
}

.members-section {
  display: flex;
  flex-direction: column;
  gap: 40px;
  margin-top: 30px;
}

.member {
  opacity: 0;
  transform: translateY(30px);
  transition: opacity 0.6s, transform 0.6s;
  background: rgba(255, 255, 255, 0.05);
  border-radius: 12px;
  padding: 20px;
  text-align: center;
  margin-bottom: 20px;
}

.member.visible {
  opacity: 1;
  transform: translateY(0);
}

.member-image {
  width: 120px;
  height: 120px;
  border-radius: 50%;
  object-fit: cover;
  margin: 0 auto 15px auto;
  display: block;
  border: 3px solid rgba(255, 255, 255, 0.2);
}

.member h3 {
  margin: 15px 0 10px 0;
  color: #e0e0e0;
  font-size: 1.4em;
}

.member p {
  font-size: 0.95em;
  color: #c0c0c0;
  line-height: 1.6;
  max-width: 700px;
  margin: 0 auto;
  text-align: justify;
}

@media (max-width: 768px) {
  .fade-section {
    width: 95%;
    padding: 20px 16px;
  }
  
  .member-image {
    width: 100px;
    height: 100px;
  }
  
  .member h3 {
    font-size: 1.2em;
  }
  
  .member p {
    font-size: 0.9em;
  }
}
</style>
