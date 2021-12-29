<template>
    <div>
      <button @click="goToPage('home')">
        Go to home
      </button>
      <h1>
        Ranking
      </h1>

      <div>
        <ul v-for="post in songs" v-bind:key="post.id">
          <li>
            Song ID: {{post.id}}
          </li>

          <li>
            Song Title: {{post.title}}
          </li>

          <li>
            Points: {{post.points}}
          </li>
        </ul>
      </div>
    </div>
</template>

<script>
    export default {
        name: "Rankingpage",
        mounted() {
          this.fetchVotes()
        },
        data() {
          return {
            songs: [],
            points: []
          }
        },
        methods: {
            goToPage(page) {
                this.$emit("change-page", page);
            },
            fetchVotes() {
              const url = "http://webservies.be/eurosong/Songs";
              fetch(url)
                .then((response) => {
                  return response.json();
                })
                .then((songs) => {
                  this.songs = songs
                })
                .then((points) => {
                  this.fetchPoints(points);
                })

            },
            fetchPoints() {
              this.songs.forEach((element, index) => {
                fetch("http://webservies.be/eurosong/Songs/" + element.id +"/points")
                .then((response) => {
                  return response.json();
                })
                .then((points)=> {
                  this.songs[index].points = points;
                })
              })
            }
        }
    }
</script>