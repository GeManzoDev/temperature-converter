<template>
  <h1>Temperature Converter</h1>
  <div class="container">
    <div class="inputField">
      <label for="degrees">Degrees</label>
      <input
        v-model="degrees"
        type="number"
        name="degrees"
        id="degrees"
        @keydown.enter="convert"
      />
    </div>
    <div class="scaleField">
      <label for="scales">Scale</label>
      <select v-model="starterScale" name="scales" id="scale">
        <option
          v-for="scale in scales"
          :value="scale.id"
          @keydown.enter="convert"
        >
          {{ scale.name }}
        </option>
      </select>
    </div>
    <div class="finalScaleField">
      <label for="finalScale">To:</label>
      <select v-model="finalScale" name="finalScale" id="finalScale">
        <option
          v-for="scale in scales"
          :value="scale.id"
          @keydown.enter="convert"
        >
          {{ scale.name }}
        </option>
      </select>
    </div>
    <button class="button" @click="convert">
      <span>Convert</span>
    </button>
    <span class="result">{{ result }} </span>
  </div>
</template>

<script>
export default {
  data() {
    return {
      degrees: 0,
      scales: [
        { name: 'celsius', id: 1 },
        { name: 'fahrenheit', id: 2 },
        { name: 'kelvin', id: 3 },
      ],
      starterScale: '',
      finalScale: '',
      result: '--',
    };
  },
  methods: {
    convert() {
      console.log(this.degrees, this.starterScale, this.finalScale);
      if (this.starterScale > 0 && this.finalScale > 0) {
        // same scale
        this.starterScale == this.finalScale
          ? (this.result = this.degrees)
          : // celsius to fahrenheit
          this.starterScale == 1 && this.finalScale == 2
          ? (this.result = this.degrees * (9 / 5) + 32)
          : // celsius to kelvin
          this.starterScale == 1 && this.finalScale == 3
          ? (this.result = this.degrees + 273.15)
          : // fahreneit to kelvin
          this.starterScale == 2 && this.finalScale == 3
          ? (this.result = parseFloat(this.degrees * (5 / 9) + 459.67).toFixed(
              2
            ))
          : // fahreneit to celsius
          this.starterScale == 2 && this.finalScale == 1
          ? (this.result = parseFloat((this.degrees - 32) * (5 / 9)).toFixed(2))
          : // kelvin to celsius
          this.starterScale == 3 && this.finalScale == 1
          ? (this.result = this.degrees - 273.15)
          : // kelvin to fahrenheit
            (this.result = ((this.degrees - 273.15) * 5) / 9 + 32);
      } else alert('Please insert scale');
      {
        {
          this.finalScale == 1
            ? (this.result += ' °C')
            : this.finalScale == 2
            ? (this.result += ' °F')
            : this.finalScale == 3
            ? (this.result += ' °K')
            : this.result;
        }
      }
    },
  },
};
</script>

<style>
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
  font-family: 'Raleway', sans-serif;
  font-weight: 300;
}
h1 {
  text-align: center;
  font-weight: 600;
  margin: 2rem;
  font-size: 50px;
}
.container {
  display: flex;
  flex-direction: column;
  flex-wrap: wrap;
  border: 1px solid #000;
  width: 40vw;
  height: auto;
  justify-content: center;
  align-items: center;
  text-align: center;
  margin: auto;
  margin-top: 4rem;
  box-shadow: 5px 8px 7px -2px rgba(0, 0, 0, 0.67);
  border-radius: 10px;
}
.inputField {
  display: flex;
  flex-direction: column;
  padding: 1rem;
  margin: 1rem;
}
.scaleField {
  display: flex;
  flex-direction: column;
  padding: 1rem;
  margin: 1rem;
}
.finalScaleField {
  display: flex;
  flex-direction: column;
  padding: 1rem;
  margin: 0.5rem;
}
.result {
  margin: 2rem;
  font-weight: 600;
  font-size: 60px;
}
#degrees {
  width: 60px;
  padding-top: 5px;
  text-align: center;
  border-top-style: hidden;
  border-right-style: hidden;
  border-left-style: hidden;
  border-bottom-style: groove;
  background-color: #eee;
}
#degrees:focus {
  outline: none;
}

#scale {
  padding: 5px;
  border-top-style: hidden;
  border-right-style: hidden;
  border-left-style: hidden;
  border-bottom-style: groove;
  background-color: #eee;
}
#scale:focus {
  outline: none;
}
#finalScale {
  padding: 5px;
  border-top-style: hidden;
  border-right-style: hidden;
  border-left-style: hidden;
  border-bottom-style: groove;
  background-color: #eee;
}
#finalScale:focus {
  outline: none;
}
label {
  margin-bottom: 10px;
}
.button {
  margin-top: 2rem;
  cursor: pointer;
  display: inline-block;
  text-align: center;
  vertical-align: middle;
  padding: 12px 24px;
  border: 1px solid #a12727;
  border-radius: 8px;
  background: #ff4a4a;
  background: -webkit-gradient(
    linear,
    left top,
    left bottom,
    from(#ff4a4a),
    to(#992727)
  );
  background: -moz-linear-gradient(top, #ff4a4a, #992727);
  background: linear-gradient(to bottom, #ff4a4a, #992727);
  -webkit-box-shadow: #ff5959 0px 0px 14px 0px;
  -moz-box-shadow: #ff5959 0px 0px 14px 0px;
  box-shadow: #ff5959 0px 0px 14px 0px;
  text-shadow: #591717 1px 1px 1px;
  font-size: 20px;
  color: #ffffff;
  text-decoration: none;
}
.button:hover,
.button:focus {
  background: #ff5959;
  background: -webkit-gradient(
    linear,
    left top,
    left bottom,
    from(#ff5959),
    to(#b62f2f)
  );
  background: -moz-linear-gradient(top, #ff5959, #b62f2f);
  background: linear-gradient(to bottom, #ff5959, #b62f2f);
  color: #ffffff;
  text-decoration: none;
}
.button:active {
  background: #982727;
  background: -webkit-gradient(
    linear,
    left top,
    left bottom,
    from(#982727),
    to(#982727)
  );
  background: -moz-linear-gradient(top, #982727, #982727);
  background: linear-gradient(to bottom, #982727, #982727);
}
.button:before {
  content: '\0000a0';
  display: inline-block;
  height: 24px;
  width: 24px;
  line-height: 24px;
  margin: 0 4px -6px -4px;
  position: relative;
  top: 0px;
  left: 0px;
  background: url('data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAABgAAAAYCAYAAADgdz34AAAACXBIWXMAAA7EAAAOxAGVKw4bAAACuklEQVRIidWVzWtUZxTGf/cyaosiWEsy98FK4wwljElmJkEQC4FgWroopeKqkFQXLly4KIJCu4ofuHEXdfwDtK4cFCYFYw3YIthQJKNkZsQvBDN3EtNGBdNkJjrHRT7sgGLu2E0vXDi85/Kc5/3dwzkO/8EjaSXQDXwKPASu+L5fAXDeV9zzvGbHcdJA7F/HeWCn7/u330tcUrOkYiwet/7ML3ZpzLf+zIDF2tpMUm7hZvU7l1RqSSYtnSvYcHlu6e3PDJgkk/SVW6d4zHGcoY8aG8N9Z35mQzRak/8smVwMNwUuIKnZcZxf1zU06NDZc3wSjRK6dqPmmzsjI4vhg6DOa7HMlC17OGX5pm67MfSHDZfnLJ0rWCweD/4PPM+LSSq2JJN2fjRvw7OVJfHsoVM2PFuxdC5vLcl2k1SU1BzUeXFzIjHvfLZi2SOnX4vPlC2dL1hre7tJKtUj/kYs2cOpeef5gm1OJOpyviwsC86LkmLvVv3fYgmHw0hql/TDu7CcHw2IRdLHkjKSXkqy1o6Ot2PJFRZbcXlYJK2RNNIUidhPJ1M2WPTnZ8qbsOSCd0sI2Oe6buLAqdN0dHYSGryGW5rELU6w4twAld07KB/cw6N79+jr7eHJ48c+8MVyR3EI6G3dto2Ori5WHU2x8mxmKTn33deUD+5h7P59+np7mJoYHwe2B5nzLhCNtsUBWJG+XJOsbmgE16Xv+x6mJsZ9oCvoEnGBf6afPQPA1FBbQA08nZzk71IJ4Hg9G8oFfv9z6Aoz09PMHttPNbIR+/ADKj3f8OLLz/nt4gWAKnA1qDgAkrZKmvt21267OvWkZjOlLg1aUyRikjKe59Wl73ieh+M4e4ET68Ph0Jbt3axeu5a7t24yev061Wo1y3zX/FVXAYCFIluBH4FOYA1wBzgDnPR9/3ld9oFX0qjtbrSC+hUAAAAASUVORK5CYII=')
    no-repeat center center transparent;
  background-size: 100% 100%;
}
@media screen and (max-width: 540px) {
  .container {
    width: 70vw;
  }
  .button {
    height: 35px;
    width: 15px;
  }
  .button span {
    display: none;
  }
  .button::before {
    top: -7px;
    left: -6px;
  }
  .result {
    font-size: 30px;
  }
}
</style>
