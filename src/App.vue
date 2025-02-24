<!-- Window is fixed, 102px, pointer cursor, gradual blurry effect on surrounding words. -->
<!--  Comprehension questions appear afterwards in the same slide -->

<template>
  <Experiment title="Reading Experiment" translate="no">
    <Screen
      :title="'Welcome'"
      class="instructions"
      :validations="{
        SubjectID: {
          minLength: $magpie.v.minLength(2),
        },
      }"
    >
      <!-- <WelcomeScreen /> -->
      <div style="width: 40em; margin: auto">
        <div style="background-color: lightgrey; padding: 10px">
          <b> Information About this Study </b>
        </div>
        <p>
          Your participation in this research study is voluntary. Please read
          the text below carefully.
          <br /><br />

          <b>What is investigated and how?</b> You are being asked to take part
          in a research study being done at the Massachusetts Institute of
          Technology. This study will help us learn about how people read. It
          will take you around 20 minutes to complete. <br /><br />

          <b>Who can participate?</b> You can participate only if you are an
          adult native speaker of English. <br /><br />

          <b>What am I supposed to do as a participant?</b> If you choose to be
          in the study, you will use the computer mouse to read sentences in
          English and answer questions about them. <br /><br />

          <b>What are my rights during participation?</b> Your participation in
          this study is voluntary. If you choose to participate, you may change
          your mind and leave the study at any time by closing the web page
          without specifying reasons and without any disadvantages. <br /><br />

          <b>What risks and benefits can I expect?</b> There are no foreseeable
          risks for participating in this study. <br /><br />

          <b>Will I be compensated for participating?</b> If you complete the
          experiment, you will be compensated for your time following the amount
          specified on Prolific. <br /><br />

          <b>What data is collected from me and how is it used?</b> During this
          study, we will track the position of your mouse on screen. The data
          from this study may be presented at scientific conferences and
          published in scientific journals, as well as in online repositories.
          All data will remain anonymous. <br /><br />

          <b> Who reviewed this study? </b> This study's protocol has been
          approved by the MIT Committee on the Use of Humans as Experimental
          Subjects. <br /><br />

          <b> General Contact: </b> thclark@mit.edu <br />
        </p>

        <br />
        <div style="background-color: lightgrey; padding: 10px">
          <b> Consent Form </b>
        </div>
        <br />
        I, the participant, confirm by clicking the button below: <br />
        <div style="padding-left: 30px">
          • I have read and understood the study information. My questions have
          been answered completely and to my satisfaction.
        </div>
        <div style="padding-left: 30px">
          • I comply with the inclusion and exclusion criteria for participation
          described above. I am aware of the requirements and restrictions to be
          observed during the study.
        </div>
        <div style="padding-left: 30px">
          • I have had enough time to decide about my participation.
        </div>
        <div style="padding-left: 30px">
          • I participate in this study voluntarily and consent that my personal
          data be used as described above.
        </div>
        <div style="padding-left: 30px">
          • I understand that I can stop participating at any moment.
        </div>
        <br />

        <tr>
          <td>Please enter your Prolific ID to continue:&nbsp;</td>
          <td>
            <input
              name="TurkID"
              type="text"
              class="obligatory"
              v-model="$magpie.measurements.SubjectID"
            />
          </td>
        </tr>
        <tr></tr>
      </div>
      <div
        v-if="
          $magpie.measurements.SubjectID &&
          !$magpie.validateMeasurements.SubjectID.$invalid
        "
      >
        <br />
        By clicking on the button below you consent to participating in this
        study:
        <!-- <br /> -->
        <button
          @click="
            $magpie.addExpData({ SubjectId: $magpie.measurements.SubjectID });
            $magpie.nextScreen();
          "
        >
          Proceed
        </button>
      </div>
    </Screen>

    <InstructionScreen :title="'Instructions'">
      <p>
        In this study, you will read sentences that may possibly contain errors,
        and write what you think the correct version of the sentence is. Unlike
        in normal reading, however, the texts will be blurred. In order to bring
        the text into focus, move your mouse over it. When you are done reading,
        click the 'Done Reading' button.
      </p>
    </InstructionScreen>

    <InstructionScreen :title="'Instructions'">
      <p>
        As you read, you may notice that some of the sentences contain mistakes.
        This is intentional.
      </p>
      <p>
        After reading each sentence, you will then be prompted to type what you
        think the intended sentence was. Please correct any mistakes you found
        in the sentence. These could be missing words, the wrong word, typos,
        filler words, etc. There may be many ways to correct a sentence, so just
        use your best judgment -- there's not one right answer.
        <b>
          For the purposes of making corrections, you can ignore punctuation and
          capitalization.
        </b>
        You will see some examples on the next page.
      </p>
    </InstructionScreen>

    <InstructionScreen :title="'Instructions'">
      <p>
        The following are some examples similar to what you might see, paired
        with examples of how you might answer.
      </p>
      <br /><br />
      <table>
        <thead>
          <tr>
            <th>Example Input</th>
            <th width="30" align="center"></th>
            <th>Example Output</th>
          </tr>
        </thead>
        <tbody>
          <tr>
            <td>my favorite dessert is ice cream .</td>
            <td width="30" align="center">→</td>
            <td>my favorite dessert is ice cream .</td>
          </tr>
          <tr>
            <td>my um favorite desert is ice creme .</td>
            <td width="30" align="center">→</td>
            <td>my favorite dessert is ice cream .</td>
          </tr>
          <tr>
            <td>boys cat sat on mat .</td>
            <td width="30" align="center">→</td>
            <td>the boy's cat sat on the mat</td>
          </tr>
        </tbody>
      </table>
      <br /><br />
      <ul>
        <li>If there's nothing wrong with the sentence, just retype it.</li>
        <li>
          If there are mistakes, type what you think the person likely meant.
        </li>
        <li>
          You don't need to include periods, commas, apostophes, or other
          punctuation (but it's OK if you do).
        </li>
      </ul>
    </InstructionScreen>

    <InstructionScreen :title="'Practice'">
      <p>
        You will now have a chance to practice with a few examples. Remember,
        the sentences will be blurred, and you need to move your mouse over the
        words to reveal them.
      </p>
    </InstructionScreen>

    <template v-for="(trial, i) of practiceTrials">
      <Screen
        :key="i"
        class="main_screen"
        :progress="i / practiceTrials.length"
      >
        <Slide>
          <form>
            <input type="hidden" class="item_id" :value="trial.item_id" />
            <input
              type="hidden"
              class="experiment_id"
              :value="trial.experiment_id"
            />
            <input
              type="hidden"
              class="condition_id"
              :value="trial.condition_id"
            />
          </form>
          <div class="oval-cursor"></div>

          <div
            v-if="showFirstDiv"
            class="readingText"
            @mousemove="moveCursor"
            @mouseleave="changeBack"
          >
            <template v-for="(word, index) of trial.text.split(' ')">
              <span :key="index" :data-index="index">
                {{ word }}
              </span>
            </template>
          </div>

          <div
            class="blurry-layer"
            style="
              opacity: 0.3;
              filter: blur(3.5px);
              transition: all 0.3s linear 0s;
            "
          >
            {{ trial.text }}
          </div>

          <div style="height: 75px"></div>

          <div>
            <button
              v-if="showFirstDiv"
              @click="toggleDivs"
              :disabled="!isCursorMoving"
            >
              Done Reading
            </button>
          </div>

          <div v-if="!showFirstDiv" class="userInput">
            <p>
              Please enter what you think the most likely intended sentence was,
              using your judgment to correct any mistakes or fill in any gaps.
              You can ignore punctuation and capitalization.
            </p>
            <TextareaInput :response.sync="$magpie.measurements.response" />
          </div>

          <button
            v-if="$magpie.measurements.response"
            @click="
              toggleDivs();
              $magpie.addTrialData({
                TrialId: i,
                ItemId: trial.item_id,
                Condition: trial.condition_id,
                Experiment: trial.experiment_id,
                TrialText: trial.text,
                TrialType: `textInputInference`,
                userResponse: $magpie.measurements.response,
              });
              $magpie.nextScreen();
            "
          >
            Next Trial
          </button>
        </Slide>
      </Screen>
    </template>

    <InstructionScreen :title="'Practice Complete'">
      <p>
        You have completed the practice questions. Press the button to start the
        experiment. Remember, there's isn't one right answer, so just use your
        best judgment!
      </p>
    </InstructionScreen>

    <template v-for="(trial, i) of trials">
      <Screen :key="i" class="main_screen" :progress="i / trials.length">
        <Slide>
          <form>
            <input type="hidden" class="item_id" :value="trial.item_id" />
            <input
              type="hidden"
              class="experiment_id"
              :value="trial.experiment_id"
            />
            <input
              type="hidden"
              class="condition_id"
              :value="trial.condition_id"
            />
          </form>
          <div class="oval-cursor"></div>

          <template>
            <div>Sentence {{ i + 1 }} of {{ trials.length }}</div>
          </template>

          <div
            v-if="showFirstDiv"
            class="readingText"
            @mousemove="moveCursor"
            @mouseleave="changeBack"
          >
            <template v-for="(word, index) of trial.text.split(' ')">
              <span :key="index" :data-index="index">
                {{ word }}
              </span>
            </template>
          </div>

          <div
            class="blurry-layer"
            style="
              opacity: 0.3;
              filter: blur(3.5px);
              transition: all 0.3s linear 0s;
            "
          >
            {{ trial.text }}
          </div>

          <div style="height: 75px"></div>

          <div>
            <button
              v-if="showFirstDiv"
              @click="toggleDivs"
              :disabled="!isCursorMoving"
            >
              Done Reading
            </button>
          </div>

          <div v-if="!showFirstDiv" class="userInput">
            <p>
              Please enter what you think the most likely intended sentence was,
              using your judgment to correct any mistakes or fill in any gaps.
              You can ignore punctuation and capitalization.
            </p>
            <TextareaInput :response.sync="$magpie.measurements.response" />
          </div>

          <button
            v-if="$magpie.measurements.response"
            @click="
              toggleDivs();
              $magpie.addTrialData({
                TrialId: i,
                ItemId: trial.item_id,
                Condition: trial.condition_id,
                Experiment: trial.experiment_id,
                TrialText: trial.text,
                TrialType: `textInputInference`,
                userResponse: $magpie.measurements.response,
              });
              $magpie.nextScreen();
            "
          >
            Next Trial
          </button>
        </Slide>
      </Screen>
    </template>

    <Screen>
      <p>1. Which input device are you using for this experiment?</p>
      <MultipleChoiceInput
        :response.sync="$magpie.measurements.device"
        orientation="horizontal"
        :options="['Computer Mouse', 'Computer Trackpad', 'Other']"
      />
      <br />
      <br />
      <p>2. Which hand are you using during this experiment?</p>
      <MultipleChoiceInput
        :response.sync="$magpie.measurements.hand"
        orientation="horizontal"
        :options="['Left', 'Right', 'Both']"
      />
      <br />
      <br />
      <p>
        What did you think about the experiment? Please describe how hard or
        easy the task felt, anything you noticed about the sentences, or any
        other thoughts you have. If anything was confusing or frustrating,
        please feel free to let us know!
      </p>
      <TextareaInput :response.sync="$magpie.measurements.response" />

      <button
        style="bottom: 30%; transform: translate(-50%, -50%)"
        @click="$magpie.saveAndNextScreen()"
      >
        Submit
      </button>
    </Screen>

    <Screen>
      <p>
        The next screen will prompt you to submit your results. There may be a
        brief loading period as your results are sent to the server. Once this
        is completed, the web page will redirect you back to Prolific. On some
        browsers, you may get an alert box asking if you are sure you want to
        leave the page. Please say Yes/OK to the this alert and you will be
        taken back to Prolific. If you run into any issues please reach out to
        us via Prolific and we will work with you to address the issue.
      </p>

      <button
        style="bottom: 30%; transform: translate(-50%, -50%)"
        @click="$magpie.nextScreen()"
      >
        Continue
      </button>
    </Screen>

    <SubmitResultsScreen />
  </Experiment>
</template>

<script>
// Load data from csv files as javascript arrays with objects
import practice from "../trials/noisy_comp_items_list_practice.csv";
import list1 from "../trials/motr_materials.csv";
import fillers from "../trials/motr_fillers.csv";
import _ from "lodash";

export default {
  name: "App",
  data() {
    // const shuffledItems = _.shuffle(list1);
    const showImages = false;

    // Create an array with 5 repeats of each value
    // 4 combinations x 5 values = 20 total items
    const conditions = _.flatMap(
      [
        "Preposition_plausible",
        "Preposition_implausible",
        "Transitive_plausible",
        "Transitive_implausible",
      ],
      (value) => _.times(5, () => value)
    );
    const shuffledConditions = _.shuffle(conditions);

    const updatedItems = list1.map((trial, idx) => {
      var col = shuffledConditions[idx];
      return {
        ...trial,
        item_id: trial["Item"],
        text: trial[col],
        condition_id: col,
        experiment_id: "trans_intrans",
      };
    });

    const updatedFillers = fillers.map((trial, idx) => {
      return {
        ...trial,
        item_id: trial["Item"],
        text: trial["Sentence"],
        condition_id: "Filler",
        experiment_id: "trans_intrans",
      };
    });

    const numFillers = 10;
    const updatedShuffledItems = _.shuffle(
      updatedItems.concat(_.sampleSize(updatedFillers, numFillers))
    );

    // console.log(updatedShuffledItems);

    // const updatedTrials = _.sampleSize(updatedShuffledItems, 3);
    return {
      isCursorMoving: false,
      practiceTrials: practice,
      trials: updatedShuffledItems,
      currentIndex: null,
      showFirstDiv: true,
      mousePosition: {
        x: 0,
        y: 0,
      },
      userResponse: "",
      showImages: showImages,
    };
  },
  computed: {},
  mounted() {
    setInterval(this.saveData, 50);
  },
  methods: {
    changeBack() {
      this.$el.querySelector(".oval-cursor").classList.remove("grow");
      this.$el.querySelector(".oval-cursor").classList.remove("blank");
      this.currentIndex = null;
    },
    saveData() {
      if (this.currentIndex !== null) {
        const currentElement = this.$el.querySelector(
          `span[data-index="${this.currentIndex}"]`
        );
        if (currentElement) {
          const currentElementRect = currentElement.getBoundingClientRect();
          $magpie.addTrialData({
            Experiment: this.$el.querySelector(".experiment_id").value,
            Condition: this.$el.querySelector(".condition_id").value,
            ItemId: this.$el.querySelector(".item_id").value,
            Index: this.currentIndex,
            Word: currentElement.innerHTML,
            mousePositionX: this.mousePosition.x,
            mousePositionY: this.mousePosition.y,
            wordPositionTop: currentElementRect.top,
            wordPositionLeft: currentElementRect.left,
            wordPositionBottom: currentElementRect.bottom,
            wordPositionRight: currentElementRect.right,
            // wordPositionTop: currentElement.offsetTop,
            // wordPositionLeft: currentElement.offsetLeft,
            // wordPositionBottom: currentElement.offsetHeight + currentElement.offsetTop,
            // wordPositionRight: currentElement.offsetWidth + currentElement.offsetLeft
          });
        } else {
          $magpie.addTrialData({
            Experiment: this.$el.querySelector(".experiment_id").value,
            Condition: this.$el.querySelector(".condition_id").value,
            ItemId: this.$el.querySelector(".item_id").value,
            Index: this.currentIndex,
            mousePositionX: this.mousePosition.x,
            mousePositionY: this.mousePosition.y,
          });
        }
      }
    },
    moveCursor(e) {
      this.isCursorMoving = true;
      this.$el.querySelector(".oval-cursor").classList.add("grow");
      let x = e.clientX;
      let y = e.clientY;
      const elementAtCursor = document.elementFromPoint(x, y).closest("span");
      if (elementAtCursor) {
        this.$el.querySelector(".oval-cursor").classList.remove("blank");
        this.currentIndex = elementAtCursor.getAttribute("data-index");
      } else {
        this.$el.querySelector(".oval-cursor").classList.add("blank");
        const elementAboveCursor = document
          .elementFromPoint(x, y - 3)
          .closest("span");
        if (elementAboveCursor) {
          this.currentIndex = elementAboveCursor.getAttribute("data-index");
        } else {
          this.currentIndex = -1;
        }
      }

      this.$el.querySelector(".oval-cursor").style.left = `${x + 12}px`;
      this.$el.querySelector(".oval-cursor").style.top = `${y - 6}px`;
      this.mousePosition.x = e.clientX;
      this.mousePosition.y = e.clientY;
      // this.mousePosition.x = e.offsetX;
      // this.mousePosition.y = e.offsetY;
    },
    toggleDivs() {
      this.showFirstDiv = !this.showFirstDiv;
      this.isCursorMoving = false;
    },
    getScreenDimensions() {
      return {
        window_inner_width: window.innerWidth,
        window_inner_height: window.innerHeight,
      };
    },
  },
};
</script>

<style>
.experiment {
  display: flex;
  align-items: center;
  justify-content: center;
}
.main_screen {
  isolation: isolate;
  position: relative;
  width: 100%;
  height: auto;
  font-size: 18px;
  line-height: 40px;
}
.debugResults {
  width: 100%;
}
.readingText {
  /* z-index: 1; */
  position: absolute;
  color: white;
  text-align: left;
  font-weight: 450;
  cursor: pointer;
  padding-top: 2%;
  padding-bottom: 2%;
  padding-left: 11%;
  padding-right: 11%;
}
.userInput {
  padding-top: 2%;
  padding-bottom: 2%;
  padding-left: 20%;
  padding-right: 20%;
}
button {
  /* position: absolute; */
  /* bottom: 0; */
  left: 50%;
}
.oval-cursor {
  position: fixed;
  z-index: 2;
  width: 1px;
  height: 1px;
  transform: translate(-50%, -50%);
  background-color: white;
  mix-blend-mode: difference;
  border-radius: 50%;
  pointer-events: none;
  transition: width 0.5s, height 0.5s;
}
.oval-cursor.grow.blank {
  width: 80px;
  height: 13px;
}
.oval-cursor.grow {
  width: 102px;
  height: 38px;
  border-radius: 50%;
  box-shadow: 30px 0 8px -4px rgba(255, 255, 255, 0.1),
    -30px 0 8px -4px rgba(255, 255, 255, 0.1);
  background-color: rgba(255, 255, 255, 0.3);
  background-blend-mode: screen;
  pointer-events: none;
  transition: width 0.5s, height 0.5s;
  filter: blur(3px);
}
.oval-cursor.grow::before {
  content: "";
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  width: 70%;
  height: 70%;
  background-color: white;
  mix-blend-mode: normal;
  border-radius: 50%;
}
.blurry-layer {
  position: absolute;
  pointer-events: none;
  color: black;
  text-align: left;
  font-weight: 450;
  padding-top: 2%;
  padding-bottom: 2%;
  padding-left: 11%;
  padding-right: 11%;
}

* {
  user-select: none; /* Standard syntax */
  -webkit-user-select: none; /* Safari */
  -moz-user-select: none; /* Firefox */
  -ms-user-select: none; /* Internet Explorer/Edge */
}
</style>
