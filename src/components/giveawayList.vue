<template>
  <section id="homeList" class="sm:bg-primary md:py-1">
    <div
      class="container p-2 py-5 mx-auto md:my-8 bg-lighter md:p-7 lg:p-10 md:rounded-lg"
    >
      <div class="items-center justify-center w-full px-2 md:p-0" id="app">
        <div v-if="loading" class="w-full mx-auto">
          <img class="mx-auto" src="/img/spinner.svg" />
        </div>
        <div v-else>
          <div
            class="p-5 mx-2 mb-5 overflow-hidden transition duration-300 transform rounded-lg shadow-sm bg-middle md:flex hover:border-indigo-200"
            id="filter"
          >
            <div class="w-full px-3 mb-6 md:w-1/3 md:mb-0">
              <label
                class="block mb-2 text-xs font-bold tracking-wide text-gray-700 uppercase"
                for="grid-state"
              >
                Platform
              </label>
              <div class="relative">
                <select
                  class="block w-full px-4 py-3 pr-8 leading-tight text-indigo-200 border border-indigo-200 border-opacity-50 rounded opacity-50 appearance-none bg-middle focus:outline-none focus:bg-lighter focus:border-gray-500"
                  id="grid-state"
                  v-model="filter.platform"
                >
                  <option value="none">All</option>
                  <option value="gleam_url">Gleam</option>
                  <option value="playr_url">Playr</option>
                  <option value="sdqk_url">Sideqik</option>
                </select>
                <div
                  class="absolute inset-y-0 right-0 flex items-center px-2 text-gray-700 pointer-events-none"
                >
                  <svg
                    class="w-4 h-4 fill-current"
                    xmlns="http://www.w3.org/2000/svg"
                    viewBox="0 0 20 20"
                  >
                    <path
                      d="M9.293 12.95l.707.707L15.657 8l-1.414-1.414L10 10.828 5.757 6.586 4.343 8z"
                    />
                  </svg>
                </div>
              </div>
            </div>
            <div class="w-full px-3 mb-6 md:w-1/3 md:mb-0">
              <label
                class="block mb-2 text-xs font-bold tracking-wide text-gray-700 uppercase"
                for="grid-state"
              >
                Verified
              </label>
              <div class="relative">
                <select
                  class="block w-full px-4 py-3 pr-8 leading-tight text-indigo-200 border border-indigo-200 border-opacity-50 rounded opacity-50 appearance-none bg-middle focus:outline-none focus:bg-lighter focus:border-gray-500"
                  id="grid-state"
                  v-model="filter.verified_twitter"
                >
                  <option value="none">Both</option>
                  <option value="yes">Yes</option>
                  <option value="no">No</option>
                </select>
                <div
                  class="absolute inset-y-0 right-0 flex items-center px-2 text-gray-700 pointer-events-none"
                >
                  <svg
                    class="w-4 h-4 fill-current"
                    xmlns="http://www.w3.org/2000/svg"
                    viewBox="0 0 20 20"
                  >
                    <path
                      d="M9.293 12.95l.707.707L15.657 8l-1.414-1.414L10 10.828 5.757 6.586 4.343 8z"
                    />
                  </svg>
                </div>
              </div>
            </div>
          </div>
          <div
            v-for="giveaway in paginatedData"
            :key="giveaway.id"
            class="w-full px-2 mb-5 transition duration-100 ease-out transform hover:-translate-y-2"
          >
            <div
              v-bind:class="{ 'opacity-25': giveaway.completed }"
              class="overflow-hidden transition duration-300 transform border-l-8 border-indigo-500 border-solid rounded-lg shadow-sm bg-middle hover:shadow-md hover:bg-primary md:flex hover:border-indigo-200"
            >
              <router-link :to="'/giveaway/' + giveaway.id" class="w-full">
                <div class="px-3 py-2 md:p-3 lg:p-4">
                  <div class="flex items-center justify-between">
                    <div class="w-full">
                      <div class="flex flex-wrap items-center">
                        <p
                          class="mr-2 text-lg font-medium tracking-widest text-indigo-200 lg:text-2xl header-font"
                        >
                          {{ giveaway.name }}
                        </p>
                        <div class="flex items-center" v-if="giveaway.boost">
                          <svg
                            class="inline-block w-4 h-4 mr-1 text-yellow-300 align-middle md:w-5 md:h-5"
                            fill="none"
                            stroke-linecap="round"
                            stroke-linejoin="round"
                            stroke-width="2"
                            viewBox="0 0 24 24"
                            stroke="currentColor"
                          >
                            <path
                              d="M11.049 2.927c.3-.921 1.603-.921 1.902 0l1.519 4.674a1 1 0 00.95.69h4.915c.969 0 1.371 1.24.588 1.81l-3.976 2.888a1 1 0 00-.363 1.118l1.518 4.674c.3.922-.755 1.688-1.538 1.118l-3.976-2.888a1 1 0 00-1.176 0l-3.976 2.888c-.783.57-1.838-.197-1.538-1.118l1.518-4.674a1 1 0 00-.363-1.118l-3.976-2.888c-.784-.57-.38-1.81.588-1.81h4.914a1 1 0 00.951-.69l1.519-4.674z"
                            />
                          </svg>
                          <p
                            class="text-xs text-yellow-300 uppercase md:text-sm"
                          >
                            Boosted Post!
                          </p>
                        </div>
                      </div>

                      <div class="flex items-center mb-2">
                        <div class="flex items-center justify-between">
                          <div class="flex flex-row-reverse justify-end">
                            <p
                              class="text-xs tracking-widest text-gray-500 md:text-sm"
                            >
                              {{ giveaway.description }}
                            </p>
                          </div>
                        </div>
                      </div>
                      <hr class="my-1 opacity-25 md:my-2" />
                      <div class="flex flex-wrap text-xs giveawayInfo">
                        <div
                          v-if="giveaway.verified_twitter"
                          class="flex flex-no-wrap items-center mr-2 text-gray-600"
                        >
                          <svg
                            class="inline w-4 h-4 mr-1 text-green-600 align-middle"
                            fill="none"
                            stroke-linecap="round"
                            stroke-linejoin="round"
                            stroke-width="2"
                            viewBox="0 0 24 24"
                            stroke="currentColor"
                          >
                            <path
                              d="M9 12l2 2 4-4M7.835 4.697a3.42 3.42 0 001.946-.806 3.42 3.42 0 014.438 0 3.42 3.42 0 001.946.806 3.42 3.42 0 013.138 3.138 3.42 3.42 0 00.806 1.946 3.42 3.42 0 010 4.438 3.42 3.42 0 00-.806 1.946 3.42 3.42 0 01-3.138 3.138 3.42 3.42 0 00-1.946.806 3.42 3.42 0 01-4.438 0 3.42 3.42 0 00-1.946-.806 3.42 3.42 0 01-3.138-3.138 3.42 3.42 0 00-.806-1.946 3.42 3.42 0 010-4.438 3.42 3.42 0 00.806-1.946 3.42 3.42 0 013.138-3.138z"
                            />
                          </svg>
                          <span
                            title="This competition host is verified on Twitter"
                            class="whitespace-no-wrap align-middle"
                            >Verified</span
                          >
                        </div>
                        <div
                          v-if="giveaway.created_at"
                          class="flex flex-no-wrap items-center mr-2 text-gray-600"
                        >
                          <svg
                            class="inline w-4 h-4 mr-1 align-middle"
                            fill="none"
                            stroke-linecap="round"
                            stroke-linejoin="round"
                            stroke-width="2"
                            viewBox="0 0 24 24"
                            stroke="currentColor"
                          >
                            <path
                              d="M8 7V3m8 4V3m-9 8h10M5 21h14a2 2 0 002-2V7a2 2 0 00-2-2H5a2 2 0 00-2 2v12a2 2 0 002 2z"
                            />
                          </svg>
                          <span class="whitespace-no-wrap align-middle"
                            >Added {{ giveaway.created_at }}</span
                          >
                        </div>
                        <div
                          v-if="giveaway.ends_at"
                          class="flex flex-no-wrap items-center mr-2 text-gray-600"
                        >
                          <svg
                            fill="none"
                            stroke-linecap="round"
                            stroke-linejoin="round"
                            stroke-width="2"
                            viewBox="0 0 24 24"
                            stroke="currentColor"
                            class="inline w-4 h-4 mr-1 align-middle"
                          >
                            <path
                              d="M12 8v4l3 3m6-3a9 9 0 11-18 0 9 9 0 0118 0z"
                            ></path>
                          </svg>

                          <span class="whitespace-no-wrap align-middle"
                            >Ends {{ giveaway.ends_at }}</span
                          >
                        </div>
                        <div
                          v-if="
                            giveaway.gleam_url ||
                              giveaway.playr_url ||
                              giveaway.sdqk_url
                          "
                          class="flex flex-no-wrap items-center mr-2 text-gray-600"
                        >
                          <svg
                            class="inline w-4 h-4 mr-1 align-middle"
                            fill="none"
                            stroke-linecap="round"
                            stroke-linejoin="round"
                            stroke-width="2"
                            viewBox="0 0 24 24"
                            stroke="currentColor"
                          >
                            <path
                              d="M13 16h-1v-4h-1m1-4h.01M21 12a9 9 0 11-18 0 9 9 0 0118 0z"
                            />
                          </svg>
                          <span
                            v-if="giveaway.gleam_url"
                            title="Giveaway hosted by gleam.io platform."
                            class="whitespace-no-wrap align-middle"
                            >Gleam Competition</span
                          >
                          <span
                            v-if="giveaway.playr_url"
                            title="Giveaway hosted by playr.gg platform."
                            class="whitespace-no-wrap align-middle"
                            >Playr Competition</span
                          >
                          <span
                            title="Giveaway hosted by sdqk.me platform."
                            v-if="giveaway.sdqk_url"
                            class="whitespace-no-wrap align-middle"
                            >Sdqk Competition</span
                          >
                        </div>

                        <div
                          v-if="giveaway.like_required"
                          class="flex flex-no-wrap items-center mr-2 text-gray-600"
                        >
                          <svg
                            class="inline w-4 h-4 mr-1 align-middle"
                            fill="none"
                            stroke-linecap="round"
                            stroke-linejoin="round"
                            stroke-width="2"
                            viewBox="0 0 24 24"
                            stroke="currentColor"
                          >
                            <path
                              d="M14 10h4.764a2 2 0 011.789 2.894l-3.5 7A2 2 0 0115.263 21h-4.017c-.163 0-.326-.02-.485-.06L7 20m7-10V5a2 2 0 00-2-2h-.095c-.5 0-.905.405-.905.905 0 .714-.211 1.412-.608 2.006L7 11v9m7-10h-2M7 20H5a2 2 0 01-2-2v-6a2 2 0 012-2h2.5"
                            />
                          </svg>

                          <span
                            title="Giveaway may require you to 'like' a tweet."
                            class="whitespace-no-wrap align-middle"
                            >Like Required</span
                          >
                        </div>

                        <div
                          v-if="giveaway.rt_required"
                          class="items-center mr-2 text-gray-600"
                        >
                          <svg
                            class="inline w-4 h-4 mr-1 align-middle"
                            fill="none"
                            stroke-linecap="round"
                            stroke-linejoin="round"
                            stroke-width="2"
                            viewBox="0 0 24 24"
                            stroke="currentColor"
                          >
                            <path
                              d="M8 12h.01M12 12h.01M16 12h.01M21 12c0 4.418-4.03 8-9 8a9.863 9.863 0 01-4.255-.949L3 20l1.395-3.72C3.512 15.042 3 13.574 3 12c0-4.418 4.03-8 9-8s9 3.582 9 8z"
                            />
                          </svg>

                          <span
                            title="Giveaway may require you to 'retweet' a tweet."
                            class="whitespace-no-wrap align-middle"
                            >Retweet Required</span
                          >
                        </div>

                        <div
                          v-if="giveaway.follow_required"
                          class="items-center mr-2 text-gray-600"
                        >
                          <svg
                            class="inline w-4 h-4 mr-1 align-middle"
                            fill="none"
                            stroke-linecap="round"
                            stroke-linejoin="round"
                            stroke-width="2"
                            viewBox="0 0 24 24"
                            stroke="currentColor"
                          >
                            <path
                              d="M11.049 2.927c.3-.921 1.603-.921 1.902 0l1.519 4.674a1 1 0 00.95.69h4.915c.969 0 1.371 1.24.588 1.81l-3.976 2.888a1 1 0 00-.363 1.118l1.518 4.674c.3.922-.755 1.688-1.538 1.118l-3.976-2.888a1 1 0 00-1.176 0l-3.976 2.888c-.783.57-1.838-.197-1.538-1.118l1.518-4.674a1 1 0 00-.363-1.118l-3.976-2.888c-.784-.57-.38-1.81.588-1.81h4.914a1 1 0 00.951-.69l1.519-4.674z"
                            ></path>
                          </svg>

                          <span
                            title="Giveaway may require you to 'follow' a user."
                            class="whitespace-no-wrap align-middle"
                            >Follow Required</span
                          >
                        </div>
                      </div>
                      <!--<div
                        class="mt-3 text-sm font-medium tracking-widest text-gray-600 md:text-lg header-font md:mt-0"
                      >
                        <img
                          v-if="giveaway.twitterProfileImage"
                          class="inline-block w-8 mr-1 rounded-full"
                          v-bind:src="giveaway.twitterProfileImage"
                        />
                        {{ giveaway.display_name }}
                      </div> -->
                    </div>
                    <!-- <router-link
                      :to="'/giveaway/' + giveaway.id"
                      class="px-1 mt-3 ml-5 font-bold text-indigo-200 transition duration-300 bg-indigo-500 rounded-lg shadow-md sm:mt-0 md:py-1 md:p-4 hover:bg-indigo-200 hover:text-indigo-800"
                    >
                      <svg
                        class="w-6 h-6 "
                        fill="none"
                        stroke-linecap="round"
                        stroke-linejoin="round"
                        stroke-width="2"
                        viewBox="0 0 24 24"
                        stroke="currentColor"
                      >
                        <path
                          d="M13 9l3 3m0 0l-3 3m3-3H8m13 0a9 9 0 11-18 0 9 9 0 0118 0z"
                        ></path></svg
                    ></router-link>-->
                  </div>
                </div>
              </router-link>
            </div>
          </div>

          <!--
          ██████╗  █████╗  ██████╗ ██╗███╗   ██╗ █████╗ ████████╗██╗ ██████╗ ███╗   ██╗
          ██╔══██╗██╔══██╗██╔════╝ ██║████╗  ██║██╔══██╗╚══██╔══╝██║██╔═══██╗████╗  ██║
          ██████╔╝███████║██║  ███╗██║██╔██╗ ██║███████║   ██║   ██║██║   ██║██╔██╗ ██║
          ██╔═══╝ ██╔══██║██║   ██║██║██║╚██╗██║██╔══██║   ██║   ██║██║   ██║██║╚██╗██║
          ██║     ██║  ██║╚██████╔╝██║██║ ╚████║██║  ██║   ██║   ██║╚██████╔╝██║ ╚████║
          ╚═╝     ╚═╝  ╚═╝ ╚═════╝ ╚═╝╚═╝  ╚═══╝╚═╝  ╚═╝   ╚═╝   ╚═╝ ╚═════╝ ╚═╝  ╚═══╝
          -->

          <div class="flex pb-5 mx-auto pagination">
            <paginator
              :data="filteredGiveaways"
              @loadedData="getPaginatedData"
            />
            <!-- <ul class="flex mx-auto mt-10">
              <li class="px-3 py-2 mx-1 text-gray-500 bg-gray-200 rounded-lg">
                <a class="flex items-center font-bold" href="#">
                  <span class="mx-1">previous</span>
                </a>
              </li>
              <li
                class="px-3 py-2 mx-1 text-gray-700 bg-gray-200 rounded-lg hover:bg-indigo-600 hover:text-gray-100"
              >
                <a class="font-bold" href="#">1</a>
              </li>
              <li
                class="px-3 py-2 mx-1 text-gray-700 bg-gray-200 rounded-lg hover:bg-indigo-600 hover:text-gray-100"
              >
                <a class="font-bold" href="#">2</a>
              </li>
              <li
                class="px-3 py-2 mx-1 text-gray-700 bg-gray-200 rounded-lg hover:bg-indigo-600 hover:text-gray-100"
              >
                <a class="font-bold" href="#">3</a>
              </li>
              <li
                class="px-3 py-2 mx-1 text-gray-700 bg-gray-200 rounded-lg hover:bg-indigo-600 hover:text-gray-100"
              >
                <a class="flex items-center font-bold" href="#">
                  <span class="mx-1">Next</span>
                </a>
              </li>
            </ul> -->
          </div>
        </div>
      </div>
    </div>
  </section>
</template>

<script>
import paginator from "../util/paginator";
var moment = require("moment");
moment().format();

export default {
  mounted() {},
  components: {
    paginator,
  },
  data() {
    return {
      filter: {
        verified_twitter: "none",
        platform: "none",
      },
      giveaways: [],
      loading: true,
      markedAsDone: [],
      paginatedData: [],
    };
  },
  computed: {
    filteredGiveaways() {
      let { platform, verified_twitter } = this.filter;
      let verified = this.deString(verified_twitter);

      let filters = [];

      if (verified !== "none")
        filters.push({ key: "verified_twitter", value: verified });
      if (platform !== "none")
        filters.push({ key: platform, value: null, op: "ne" });

      return this.giveaways.filter((gw) => {
        return filters.every(({ key, value, op }) => {
          return op && op === "ne" ? gw[key] !== value : gw[key] === value;
        });
      });
    },
  },
  methods: {
    getPaginatedData(value) {
      this.paginatedData = value;
    },
    deString(value) {
      return {
        none: "none",
        yes: true,
        no: false,
      }[value];
    },
    async getAllGiveAways() {
      try {
        await fetch(
          "https://api.comps.gg/giveaways?published=true&_sort=created_at:desc"
        )
          .then((response) => response.json())
          .then((data) => {
            this.giveaways = data.map((item) => ({
              ...item,
              created_at: moment(item.created_at).format("DD/MM/YY"),
              ends_at: item.end_date
                ? moment(item.end_date).format("DD/MM/YY HH:MM")
                : "",
            }));
            let markedAsDone = localStorage.getItem("markedAsDone");

            if (markedAsDone != null) {
              this.giveaways.forEach(function(item) {
                item.completed = markedAsDone.includes(item.id);
              });
            }

            this.giveaways.sort((a, b) => Number(b.boost) - Number(a.boost));

            this.loading = false;
          });
      } catch (err) {
        console.log(err);
      }
    },
  },
  created() {
    this.getAllGiveAways();
  },
};
</script>

<style scoped>
button:disabled {
  cursor: default;
}
</style>
