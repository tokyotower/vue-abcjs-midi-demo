<template>
	<div class="hello">
		<!-- <div class="listener-output">
			<div class="label">Currently Playing:
				<span class="abc-string">{{currentAbcFragment}}</span>
			</div>

			<div class="label">Parameters sent to listener callback: </div>
			<div>Progress: {{progress.progress }}</div>
			<div>Current Time: {{progress.currentTime }}</div>
			<div>Total Duration: {{progress.duration }}</div>
			<div>New Beat? {{progress.newBeat }}</div>
		</div> -->
		<div id="midi"></div>
		<div id="paper"></div>
		<textarea id="abc-source" v-model="tune"></textarea>
	</div>
</template>

<script>
import "font-awesome/css/font-awesome.min.css";
import "abcjs/abcjs-midi.css";
import abcjs from "abcjs/midi";

export default {
  mounted: function() {
    new abcjs.Editor("abc-source", {
      canvas_id: "paper",
      generate_midi: true,
      midi_id: "midi",
      abcjsParams: {
        midiListener: this.listener,
        animate: {
          listener: this.animate
        },
        format: {
          gchordfont: "kokoro",
          annotationfont: "kokoro",
          composerfont: "kokoro",
          footerfont: "kokoro",
          headerfont: "kokoro",
          historyfont: "kokoro",
          infofont: "kokoro",
          measurefont: "kokoro",
          partsfont: "kokoro",
          repeatfont: "kokoro",
          subtitlefont: "kokoro",
          tempofont: "kokoro",
          textfont: "kokoro",
          titlefont: "kokoro",
          voicefont: "kokoro",
          vocalfont: "kokoro",
          wordsfont: "kokoro"
        }
      }
    });
  },
  name: "hello",
  data() {
    return {
      progress: {},
      currentAbcFragment: "(none)",
      tune:
        'X:1\nT: 南山小学校校歌\nM: 4/4\nL: 1/8\nQ: 1/4=115\nK: Bb\n[V: Top clef=treble name="あんな" snm="あ"]\nF2||:B3cd2B2|F4D2 G3/2A1/2|B3cB2G2|F4z2B2|\nw:あ ざ ぶ の お か に そ び え て た て る こ\nw:* な み の や ま の か が や く れ き し ほ\n[V: 2nd clef=treble name="あすか" snm="あ"]\nF2||:B3cd2B2|F4D2 G3/2A1/2|G3GF2F2|D4z2F2|\nw:あ ざ ぶ の お か に そ び え て た て る フ\nw:* な み の や ま の か が や く れ き し フ\n[V: 3rd clef=treble-8 name="りょうご" snm="り"]\nF2||:B3cd2B2|F4D2 G3/2A1/2|d3dc2c2|A4z2B2|\nw:あ ざ ぶ の お か に そ び え て た て る フ\nw:* な み の や ま の か が や く れ き し フ\n[V: 4th clef=treble-8 name="はるき" snm="ぶ"]\nF2||:B3cd2B2|F4D2 G3/2A1/2|B3cB2G2|F4z2G2|\nw:あ ざ ぶ の お か に そ び え て た て る フ\nw:* な み の や ま の か が や く れ き し フ\n[V: 5th clef=bass name="けいた" snm="け"]\nF,2||:B,,3B,,B,,2B,,2|D,4D,2 D,3/2D,1/2|E,3E,E,2E,2|D,4G,,2z2|\nw:あ ざ ぶ の お か に そ び え て た て る \nw:* な み の や ま の か が や く れ き し ー\n[V: Top]\nG3cB2D2|F3GF2 B3/2B1/2|F3DD2C2|B,6C2||\nw:う しゃ を め ぐ ー る き ぎ の わ か め の し\nw:し ー の き しょう ー の そ ら す み わ た る は\n[V: 2nd]\nG4G4|F4F2F3/2F1/2|B,3B,B,2B,2|zG -GF -FD3||\nw:ウ ー ウ ー き ぎ の わ か め ウォウ ー ウォウ ー ウォウ\nw:ウ ー ウ ー そ ら す み わ た ウォウ ー ウォウ ー ウォウ\n[V: 3rd]\nd4d2c2|c2d2d2d3/2d1/2|G3GG2G2|zd -dc -cB3||\nw:ウ ー ー ウ ー ー き ぎ の わ か め ウォウ ー ウォウ ー ウォウ\nw:ウ ー ー ウ ー ー そ ら す み わ た ウォウ ー ウォウ ー ウォウ\n[V: 4th]\nB4B4|A2c2B2B3/2B1/2|E3EE2E2|zB -BA -AF3||\nw:ウ ー ウ ー ー き ぎ の わ か め ウォウ ー ウォウ ー ウォウ\nw:ウ ー ウ ー ー そ ら す み わ た ウォウ ー ウォウ ー ウォウ\n[V: 5th]\nE,4 E,4|D,4 G,,4|C,4 F,,4|B,,8||\n[V: Top]\nC3C CF2E|D2F2z2B3/2A1/2|G3GG2c2|c6 d3/2c1/2|\nw:じ に の び ー ゆ く わ れ ら が す が た お お\nw:て な き ー そ ら は わ れ ら が こ こ ろ お お\n[V: 2nd]\nA8|B4z2G3/2F1/2|=E3EE2G2|z8||\n[V: 3rd]\nf8|f4z4|c3cc2=e2|z8||\n[V: 4th]\nc8|B4z4|B3AB2c2|z8||\n[V: 5th]\nE,8|D,8|C,4 =E,,4|F,,8||\n[V: Top]\nB3B cB2G|F6 B3/2B1/2|F3D D2C2|B,6 z2||\nw:す く す く ー と の び ゆ く す が た\nw:ひ ろ び ろ ー と は て な き こ こ ろ\n[V: 2nd]\nd4c4|c4d4|e4=f4|e8||\n[V: 3rd]\nB4A4|A4B4|B4B4|B8||\n[V: 4th]\nG4F4|F4F4|G4G4|G8||\n[V: 5th]\nE,4 E,4|D,4 G,,4|C,4 F,,4|B,,8||\n[V: Top]\nF3/2G1/2 FD FB2c|d6 G3/2G1/2|F3d c2c2|B6 F2:|]\nw:た の し く ま な ー ぶ わ れ ら は こ こ に み\nw:む つ み て は げ ー む わ れ ら は こ こ に *\n[V: 2nd]\nd8|d8|d4e4|d8:|]\n[V: 3rd]\nB8|B8|B4c4|B8:|]\n[V: 4th]\nF8|F8|F4A4|F8:|]\n[V: 5th]\nB,,8|z1 B,,2C,1D,4|B,,4 F,,4|B,,8:|]\n'
    };
  },
  methods: {
    listener(midiControl, progress) {
      // This provides a more linear view of the progress, for a progress bar or for an unrelated animation.
      this.progress = progress;
    },
    colorRange(range, color) {
      if (range && range.elements) {
        range.elements.forEach(function(set) {
          set.forEach(function(item) {
            item.setAttribute("fill", color);
          });
        });
      }
    },
    animate(lastRange, currentRange) {
      // This provides the actual visual note being played. It can be used to create the "bouncing ball" effect.
      this.colorRange(lastRange, "#000000"); // Set the old note back to black.
      this.colorRange(currentRange, "#3D9AFC"); // Set the currently sounding note to blue.
      if (currentRange)
        this.currentAbcFragment = this.tune.substring(
          currentRange.startChar,
          currentRange.endChar
        );
      else this.currentAbcFragment = "(none)";
    }
  }
};
</script>

<style>
.hello {
  text-align: left;
}
#abc-source {
  width: 460px;
  height: 160px;
  padding: 6px;
}

.listener-output {
  border: 1px solid #888888;
  padding: 6px;
  border-radius: 4px;
  width: 460px;
  margin-bottom: 20px;
}

.abc-string {
  border: 1px solid #e9ef96;
  padding: 2px;
  height: 24px;
  width: 60px;
  display: inline-block;
  background: #fbf4b8;
}

pre {
  border: 1px solid #888888;
  padding: 6px;
  border-radius: 4px;
  width: 460px;
}

#midi {
  width: 756px;
}

.label {
  font-weight: bold;
}
</style>
