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
        'X:1\nT: 南山小学校校歌\nM: 4/4\nL: 1/8\nQ: 1/4=105\nK: Bb\n[V: Top clef=treble name="あんな" snm="あ"]\nF2||:B3cd2B2|F4D2 G3/2A1/2|B3cB2G2|F4z2B2|\nw:あ ざ ぶ の お か に そ び え て た て る こ\nw:* な み の や ま の か が や く れ き し ほ\n[V: 2nd clef=treble name="あすか" snm="あ"]\nF2||:B3cd2B2|F4D2 G3/2A1/2|G3GG2G2|F4z2G2|\nw:あ ざ ぶ の お か に そ び え て た て る こ\nw:* な み の や ま の か が や く れ き し ほ\n[V: 3rd clef=bass name="りょうご" snm="り"]\nF,2||:B,3CD2B,2|F,4D,2 G,3/2A,1/2|B,3B,C2C2|D4z2E2|\nw:あ ざ ぶ の お か に そ び え て た て る こ\nw:* な み の や ま の か が や く れ き し ほ\n[V: 4th clef=bass name="はるき" snm="ぶ"]\nF,2||:B,3CD2B,2|F,4D,2 G,3/2F,1/2|E,3E,E,2E,2|C,4z2C2|\nw:あ ざ ぶ の お か に そ び え て た て る こ\nw:* な み の や ま の か が や く れ き し ほ\n[V: 5th clef=bass name="けいた" snm="け"]\nF,2||:E,3E,E,2E,2|D,4D,2 D,3/2D,1/2|C,3C,C,2C,2|B,,3C,D,2F,2|\nw:あ ざ ぶ の お か に そ び え て た て る ー ー こ\nw:* な み の や ま の か が や く れ き し ー ー ほ\n[V: Top]\nG3cB2D2|F3GF2 B3/2B1/2|F3DD2C2|B,6C2||\nw:う しゃ を め ぐ ー る き ぎ の わ か め の し\nw:し ー の き しょう ー の そ ら す み わ た る は\n[V: 2nd]\nE3AG2B,2|D3ED2 G3/2F1/2|B,3B,B,2B,2|B,6z2||\nw:う しゃ を め ぐ ー る き ぎ の わ か め の し\nw:し ー の き しょう ー の そ ら す み わ た る は\n[V: 3rd]\nD3DD2D2|C3CC2 C3/2C1/2|G,3G,G,2G,2|F,6z2||\nw:う しゃ を め ぐ ー る き ぎ の わ か め の し\nw:し ー の き しょう ー の そ ら す み わ た る は\n[V: 4th]\nB,3B,B,2B,2|B,3CB,2 B,3/2B,1/2|E,3E,E,2E,2|F,6z2||\nw:う しゃ を め ぐ ー る き ぎ の わ か め の し\nw:し ー の き しょう ー の そ ら す み わ た る は\n[V: 5th]\nE,3E,E,2E,2|D,3D,D,2 D,3/2D,1/2|C,3C,F,,2F,,2|B,,6z2|\nw:う しゃ を め ぐ ー る き ぎ の わ か め の し\nw:し ー の き しょう ー の そ ら す み わ た る は\n[V: Top]\nC3C CF2E|D2F2z2B3/2A1/2|G3GG2c2|c6 d3/2c1/2|\nw:じ に の び ー ゆ く わ れ ら が す が た お お\nw:て な き ー そ ら は わ れ ら が こ こ ろ お お\n[V: 2nd]\nz4A4|B4z2G3/2F1/2|=E3EE2G2|G4F2z2||\nw:フ ウ わ れ ら が す が た ー お お\nw:フ ウ わ れ ら が こ こ ろ ー お お\n[V: 3rd]\nz6C2|D4z2 D3/2C1/2|B,3B,B,2E2|E4C2z2||\nw:フ ウ わ れ ら が す が た ー お お\nw:フ ウ わ れ ら が こ こ ろ ー お お\n[V: 4th]\nz2F,2A,2G,2|F,4z2 F,3/2F,1/2|D,3D,G,2B,2|B,4A,2z2||\nw:フ ウ ウ ウ わ れ ら が す が た ー お お\nw:フ ウ ウ ウ わ れ ら が こ こ ろ ー お お\n[V: 5th]\nE,8|D,8|C,4 =E,,4|F,,8||\n[V: Top]\nB3B cB2G|F6 B3/2B1/2|F3D D2C2|B,6 z2||\nw:す く す く ー と の び ゆ く す が た\nw:ひ ろ び ろ ー と は て な き こ こ ろ\n[V: 2nd]\nF4F4|B4F4|G4G4|F8||\n[V: 3rd]\nD4D4|C4C4|E4E4|D8||\n[V: 4th]\nC4C4|G,4G,4|B,4B,4|B,8||\n[V: 5th]\nD,3D, D,D,2D,|E,6 E,3/2E,1/2|F,,3F,,F,,2^F,,2|G,,6 z2||\nw:す く す く ー と の び ゆ く す が た\nw:ひ ろ び ろ ー と は て な き こ こ ろ\n[V: Top]\nF3/2G1/2 FD FB2c|d6 G3/2G1/2|F3d c2c2|B6 F2:|]\nw:た の し く ま な ー ぶ わ れ ら は こ こ に み\nw:む つ み て は げ ー む わ れ ら は こ こ に *\n[V: 2nd]\nd8|d8|d4e4|d8:|]\n[V: 3rd]\nB,8|B,8|B,4C4|B,8:|]\n[V: 4th]\nF,8|F,8|F,4A,4|F,8:|]\n[V: 5th]\nC,4F,,4|E,,4G,,4|C,4 F,,4|B,,8:|]\n'
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
