<template>
    <div>
        <video class="demo-video" ref="player" muted autoplay></video>
        <video class="demo-video" ref="player1" muted autoplay></video>
    </div>
</template>
<script>
import flvjs from "flv.js";
export default {
    data () {
        return {
          productLists: [
            {
              id: "1",
              rtsp: "rtsp://localhost/0210test6",
              player: null
            },{
              id: "2",
              rtsp: "rtsp://localhost/0210test1",
              player1: null
            }
          ]
        }
    },
    mounted () {
        if (flvjs.isSupported()) {
            let video = this.$refs.player;
            if (video) {
                this.player = flvjs.createPlayer({
                    type: "flv",
                    isLive: true,
                    url: `ws://localhost:8888/rtsp/${this.productLists[0].id}/?url=${this.productLists[0].rtsp}`
                });
                this.player.attachMediaElement(video);
                try {
                    this.player.load();
                    this.player.play();
                } catch (error) {
                    console.log(error);
                };
            }
            let video1 = this.$refs.player1;
            if (video1) {
              this.player1 = flvjs.createPlayer({
                type: "flv",
                isLive: true,
                url: `ws://localhost:8888/rtsp/${this.productLists[1].id}/?url=${this.productLists[1].rtsp}`
              });
              this.player1.attachMediaElement(video1);
              try {
                this.player1.load();
                this.player1.play();
              } catch (error) {
                console.log(error);
              };
            }
            // if (video) {
            //     this.player = flvjs.createPlayer({
            //         type: "flv",
            //         url: `/static/test.flv`
            //     });
            //     this.player.attachMediaElement(video);
            //     try {
            //         this.player.load();
            //         this.player.play();
            //     } catch (error) {
            //         console.log(error);
            //     };
            // }
        }
    },
    beforeDestroy () {
        this.player.destory();
    }
}
</script>
<style>
    .demo-video {
        max-width: 880px;
        max-height: 660px;
    }
</style>
