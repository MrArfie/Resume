<template>
  <v-card
    color="grey lighten-4"
    light
  >
    <v-card-text>
      <content-section
        id="timeline"
        :title="detailed ? 'My Life in a Nutshell' : 'My Experiences'"
      >
        <template slot="actions">
          <div>
            <v-switch
              v-model="detailed"
              :label="detailed ? 'Detailed' : 'Summary'"
            />
          </div>
        </template>

        <v-timeline
          dense
        >
          <v-timeline-item
            v-for="(item, i) in orderedItems"
            :key="i"
            :icon="item.icon || ''"
            :class="{transparent: item.transparent}"
            large
          >
            <template
              v-if="item.iconImage"
              v-slot:icon
            >
              <v-avatar>
                <img
                  :src="publicPath(item.iconImage)"
                >
              </v-avatar>
            </template>
            <template v-slot:opposite />
            <v-layout>
              <v-flex
                v-if="$vuetify.breakpoint.smAndUp"
                md1
                sm2
                align-self-center
              >
                <span>{{ item.year }}</span>
              </v-flex>
              <v-flex
                md11
                sm10
                xs12
              >
                <v-card class="elevation-1">
                  <v-card-title class="pb-0">
                    <div>
                      <p v-if="$vuetify.breakpoint.xsOnly">
                        {{ item.year }}
                      </p>
                      <h3>{{ item.title }}</h3>
                    </div>
                  </v-card-title>
                  <v-card-text>
                    <v-layout wrap>
                      <v-flex
                        :md7="!!item.image"
                        :md12="!item.image"
                        xs12
                      >
                        <div class="mr-1">
                          <span
                            v-if="item.text"
                            class="pre"
                          >{{ item.text }}</span>
                          <!-- eslint-disable vue/no-v-html -->
                          <div
                            v-else-if="item.html"
                            v-html="item.html"
                          />
                          <!-- eslint-enable vue/no-v-html -->
                        </div>
                      </v-flex>
                      <v-flex
                        v-if="item.image"
                        md5
                        xs12
                      >
                        <div
                          class="mt-2"
                        >
                          <v-carousel
                            v-if="Array.isArray(item.image)"
                            :show-arrows="false"
                            :height="325"
                          >
                            <v-carousel-item
                              v-for="(citem,ci) in item.image"
                              :key="ci"
                              :src="publicPath(citem)"
                            />
                          </v-carousel>
                          <v-img
                            v-else
                            :max-height="item.imageHeight ? item.imageHeight : ''"
                            :src="publicPath(item.image)"
                          />
                        </div>
                      </v-flex>
                    </v-layout>
                  </v-card-text>
                </v-card>
              </v-flex>
            </v-layout>
          </v-timeline-item>
        </v-timeline>
      </content-section>
    </v-card-text>
  </v-card>
</template>

<script>
import ContentSection from '@/views/dark-template/content/Section';
export default {
  name      : 'Timeline',
  components: { ContentSection },
  data      : () => ({
    detailed: true,
    items   : [
      {
        detailed   : true,
        transparent: true,
        year       : '1998',
        title      : 'Born on January 8, 1998',
        html       : 'With a chance of %0.00000000000512.<br>I\'m completely aware of value of the life!',
        icon       : 'mdi-cake-variant',
      },
      {
        detailed   : true,
        transparent: true,
        year       : '2003',
        title      : 'Touched a Mouse',
        html       : 'ME: "Woooow!"<br><i>... Of course got slapped later!</i>',
        icon       : 'mdi-mouse-variant',
      },
      {
        detailed   : true,
        year       : '2009',
        transparent: true,
        title      : 'Started Learning in Hardware and Software Troubleshooting',
        html       : `
                <p>
                    I remember when our PC Broke we always call a technitian and while they repair it I always ask questions and watching them how to perform it.
                </p>
                <p>
                    Back then, I eventually tried reparing our PC when it broke and thus Trial error has became my concept in life 
                </p>
                <p>
                    During 2009 - 2011, many other Games and Software I've played and tried. For example:
                    <ul>
                        <li>
                            Red Alert and Yuri's Revenge
                        </li>
                        <li>
                            Facebook.com
                        </li>
                        <li>
                          Command and conquer Generals
                        </li>
                        <li>
                            And many other Games and Website I can't really remember!
                        </li>
                    </ul>
                </p>
        `,
      
        imageHeight: 200,
        icon       : 'mdi-web',
      },
      
      {
        detailed   : true,
        year       : '2011',
        transparent: true,
        title      : 'Fished Mobsters!',
        html       : `
          <p>
            Oh shouldn't I include this one?! whatever ...<br>
            It was 2011 and I'd been addicted to a game called Street Mobsters. On its US server, I decided to perform a phishing attack and harvest credentials of in-game wealthy people.
          </p>
          <p>
            I hosted a page similar to this one and published it inside the game via various mediums. To be honest, I didn't expect any result but about 40 people had given me their username and passwords! among them, I selected wealthiest ones and ... you know rest of the story just add a Robin Hood at the end!
          </p>
          <p>
            This was the moment I realized how it is easy to actually get misused especially on the net.
          </p>
        `,
        image    : 'img/timeline/street-mobsters.jpg',
        iconImage: 'img/timeline/street-mobsters-icon.png',
      },
      {
        detailed   : true,
        year       : '2012',
        transparent: true,
        title      : 'Created a Botnet',
        html       : `
                <p>
                    A VB6-based (yes you read it correctly! Visual Basic 6) botnet with dynamic C&Cs on Blogfa.com and many zombies. Just kidding, there were 3 infected PCs only!
                </p>
                <p>
                    It was initially created to perform fraud clicks on one of PPC ads on one of my old blogs. It was designed in a way that the advertiser would not be able to detect the fraud easily.
                </p>
                `,
        icon: 'mdi-desktop-classic',
      },
      
      {
        detailed   : true,
        year       : '2014-15',
        transparent: true,
        title      : 'Created a Captcha Solving Farm',
        /* eslint-disable no-useless-escape */
        html       : `
                <p>
                    I was inspired by a blog post about captcha solving techniques and made my own captcha solving farm and built some basic APIs for <span style="background-color: #d1d1d1;">/(bad)?/g</span> guys to use it.
                </p>
                <p>
                    It was initially created to make me millionaire (!) however, it was never even published since I couldn't find a way to receive money from outside of Iran. It was a stupid attempt in fact! 🤦‍♂️
                </p>
                `,
        /* eslint-enable no-useless-escape */
        icon: 'mdi-worker',
      },
      
      {
        year : '2016',
        title: 'Started Industrial Engineering in Don Honorio Ventura State Univerisity',
        html : `
          <p>
              Current status: <span class="orange--text lighten-1">Transfered</span>,
              YEARS: <span class="">4 Years(s) (variable)</span>
          </p>
          <p>
              The purpose of attending in this school is  looking for other option or perspective on my life and by doing so i realized that Engineering is not my Forte
          </p>
          <p>
              The reason behind persuing Industrial Eng. was pretty simple: it is th mother Course for Engineering and Considered as a Jack of all trades.
          </p>
          <p>
            <span class="orange--text lighten-1">Failing Reason</span>:
             A year later, I found myself in a stagnated situation thats why i transferred schools and shifted courses
          </p>
        `,
        image    : 'img/timeline/dhvtsy.jpg',
        iconImage: 'img/timeline/bobet.ir-icon.png',
      },
      {
        year       : '2017',
        transparent: true,
        title      : 'Founded Telepad',
        html       : `
          <p>
              Current status: <span class="red--text darken-3">Failed</span>,
              Team: <span class="">1</span>
          </p>
          <p>
            Telepad was a Telegram assistant bot which helped channel owners to manage their posts easily by scheduling posts, instant editing, ready-to-be-published post suggestions and administrators' role management.
          </p>
          <p>
            The reason behind founding it was personal usage. It was initially created to make Bobet.ir publishing process easier but I decided to let others use it too.
          </p>
          <p>
            <span class="red--text darken-3">Failing Reason</span>:
             Well, I was alone and couldn't handle its development since I'd been working on other projects too.<br />
             Starting from there, slowly, I understood the actual value of having a team and focusing on a specific business.
          </p>
        `,
        iconImage: 'img/timeline/telepad-icon.png',
      },
      {
        year : '2017',
        title: 'Tried to Create J.A.R.V.I.S Simulation',
        html : `
          <p>
              Current status: <span class="red--text accent-4">Failed</span>,
              Team: <span class="">1</span>
          </p>
          <p>
            I've succesfully created a semi Jarvis system on my laptop wayback in highschool days.
          </p>
          <p>
            The reason I tried to create this due to my amazed in the IRON MAN movies and I've succesfully integrated it in my laptop  
          </p>
          <p>
            JARVIS AI functions are Research,Simple Laptop Windows commands and small Conversation to the owner of the laptop
          </p>
          <p>
            <span class="red--text accent-4">Failing Reason:</span> Laptop Harddrive Burned and I dont have the main back up for the code
          </p>
        `,
        image    : 'img/timeline/jarvis.jpg',
        iconImage: 'img/timeline/delix.ir-icon.png',
      },
      {
        detailed   : true,
        transparent: true,
        year       : '2018',
        title      : 'A Turning Point',
        html       : `
          <p>
          It looks like that 2018 is missing from my CV isn't it? <strong>NOT AT ALL!</strong>
          </p>
          <p>
          This awesome year was a turning point in my life. I found out the reason why my businesses are not growing; what I'm doing wrong; what I've supposed to do and plenty of other thoughts.
          </p>
          <p>
          Technically, I got familiar with and tried to be best (not yet of course!) at the following technologies:
          <ul>
          <li>git</li>
          <li>Laravel</li>
          <li>Vue.js</li>
          <li>Arduino</li>
          <li>Ubuntu</li>
          <li>TTD and CI/CD</li>
          <li>Development best practices</li>
          <li>And more ...</li>
          </ul>
          </p>
          <p>
          So please don't underestimate this card by its height in pixels. It's worth a lot to me.
          </p>

        `,
        icon: 'mdi-cake-variant',
      },

      
      {
        year : '2019',
        title: '1st time working in BPO industries',
        html : `
          <p>
              Current status: <span class="light-blue--text lighten-3">Published</span><br>Available on: <a target="_blank" 
          </p>
          <p>
            Worked as a Call center agent for 6 Months and promoted to supervisor:
            <ul>
                <li>Supervisor from the 3 diffferent accounts/department</li>
                <li>collection.</li>
                <li>Retail.</li>
                <li>Technical</li>
            </ul>
          </p>
        `,
        image    : 'img/timeline/iqor.png',
        iconImage: 'img/timeline/vue-registrar-logo.png',
      },
      {
        year : 'So far ...',
        title: 'IT Manager from a Accounting Firm in USA',
        html : `I'm the guy who loves Coding! So far, I've handle many different project which most of them are computer-related. .</li></ul>`,
        icon: 'mdi-fountain-pen-tip',

        image    : 'img/timeline/iqor.png',
        iconImage: 'img/timeline/vue-registrar-logo.png',
      },
    ],
  }),
  computed: {
    orderedItems () {
      const items = [...this.items].reverse()
      if (this.detailed)
        return items
      return items.filter((item) => {
        return !item.detailed
      })
    },
  },
}
</script>

<style scoped>
.title {
  border-bottom: 2px #bfbfbf solid;
  line-height: 1.5 !important;
}
.pre {
  white-space: pre;
}
.transparent{
  opacity: 0.6;
}
</style>
