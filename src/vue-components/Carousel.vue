<template>
    <div>
        <button @click="changeIndex(-1)">
            prev song
        </button>

        <div v-for="(song,index) in items" :key="song.id"> 
            <div v-if="index == activeIndex">
                {{song.artist.name}} - {{song.title}}
                <iframe :src="song.spotify" width="100%" height="80" frameBorder="0" allowfullscreen="" allow="autoplay; clipboard-write; encrypted-media; fullscreen; picture-in-picture"></iframe>
            </div>
      </div>
    <button @click="changeIndex(1)">
        next song
    </button>
    </div>
</template>

<script>
    export default{
        name:"Carousel",
        props: [
            "items",
            "activeIndex"
        ],
        methods: {
            changeIndex(value) {
                //copy, you can not change props directly
                let index = this.activeIndex;
                
                // -1 of 1
                index+= value;
                //check if index is the beginning of ending. mag niet onder 0 gaan of groter dan het aantal songs
                if(index < 0) {
                    index = this.items.length-1;
                } else if (index == this.items.length) {
                    index = 0;
                }
                //change index
                this.$emit("change-index",index);
                console.log(index)
            }
        }
    }
</script>
