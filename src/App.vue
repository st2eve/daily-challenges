<!-- eslint-disable vue/no-side-effects-in-computed-properties -->
<script>
export default {
  data() {
    return {
      multiple1: 0,
      multiple2: 0,
      answer1: 0,
      fibonacciNb: 34,
      answer2: 0,
      n: [0, 1],
      palOrNot: "",
      answer3: "",
      sortArray: 0,
      answer4: [],
      addArrayOne: "",
      addArrayTwo: "",
      arrayOne: [],
      arrayTwo: [],
      answer5: [],
    };
  },
  methods: {
    resultExo1() {
      for (let i = 0; i < 1000; i++) {
        if (i % this.multiple1 == 0 || i % this.multiple2 == 0) {
          this.answer1 += i;
        }
      }
    },
    resultExo3() {
      const palArray = this.palOrNot.split("");
      const reversePalArray = palArray.reverse();
      const convertArray = reversePalArray.join("");

      if (this.palOrNot == convertArray) {
        this.answer3 = "It is a palindrome";
      } else {
        this.answer3 = "It is not a palindrome";
      }
    },
    resultExo4() {
      if (
        this.answer4.length == 0 ||
        (this.answer4.length == 1 && this.sortArray > this.answer4[0]) ||
        this.sortArray > this.answer4[this.answer4.length - 1]
      ) {
        this.answer4.push(this.sortArray);
      } else if (
        (this.answer4.length == 1 && this.sortArray < this.answer4[0]) ||
        this.sortArray < this.answer4[0]
      ) {
        this.answer4.unshift(this.sortArray);
      } else {
        for (let i = 0; i < this.answer4.length; i++) {
          if (
            this.answer4[i] < this.sortArray &&
            this.sortArray < this.answer4[i + 1]
          ) {
            this.answer4.splice(i + 1, 0, this.sortArray);
            break;
          } else if (
            this.answer4[i] > this.sortArray &&
            this.sortArray > this.answer4[i - 1]
          ) {
            this.answer4.splice(i - 1, 0, this.sortArray);
            break;
          } else if (this.answer4[i] == this.sortArray) {
            alert("This number is already in the array");
            break;
          }
        }
      }
    },
    addNbArrayOne() {
      this.arrayOne.push(this.addArrayOne);
    },
    addNbArrayTwo() {
      this.arrayTwo.push(this.addArrayTwo);
    },
    resultExo5() {
      this.answer5 = [...this.arrayOne, ...this.arrayTwo];
      const answer5 = this.answer5;

      function swap(answer5, leftIndex, rightIndex) {
        let temp = answer5[leftIndex];
        answer5[leftIndex] = answer5[rightIndex];
        answer5[rightIndex] = temp;
      }
      function partition(answer5, left, right) {
        let pivot = answer5[Math.floor((right + left) / 2)], //middle element
          i = left, //left pointer
          j = right; //right pointer
        while (i <= j) {
          while (answer5[i] < pivot) {
            i++;
          }
          while (answer5[j] > pivot) {
            j--;
          }
          if (i <= j) {
            swap(answer5, i, j); //sawpping two elements
            i++;
            j--;
          }
        }
        return i;
      }

      function quickSort(answer5, left, right) {
        let index;
        if (answer5.length > 1) {
          index = partition(answer5, left, right); //index returned from partition
          if (left < index - 1) {
            //more elements on the left side of the pivot
            quickSort(answer5, left, index - 1);
          }
          if (index < right) {
            //more elements on the right side of the pivot
            quickSort(answer5, index, right);
          }
        }
        return answer5;
      }
      // first call to quick sort
      this.answer5 = quickSort(answer5, 0, answer5.length - 1);

      Array.prototype.getUnique = function () {
        let uniques = [];
        for (let i = 0, l = this.length; i < l; ++i) {
          if (this.lastIndexOf(this[i]) == this.indexOf(this[i])) {
            uniques.push(this[i]);
          }
        }
        return uniques;
      };

      this.answer5 = answer5.getUnique();
    },
  },
  computed: {
    resultExo2() {
      for (let i = 2; this.n.length < this.fibonacciNb; i++) {
        this.n.push(this.n[i - 1] + this.n[i - 2]);
      }
      for (let i = 0; i < this.n.length; i++) {
        if (this.n[i] % 2 == 0 && this.n[i] < 4000000) {
          this.answer2 += this.n[i];
        }
      }
      return this.answer2;
    },
  },
};
</script>

<template>
  <main class="container__main">
    <div class="main__exo1">
      <h2>
        Find the sum of all the multiples of {{ multiple1 }} or
        {{ multiple2 }} below 1000
      </h2>
      <div class="form__multiples">
        <label> Multiple 1 : </label>
        <input class="multiples" type="number" v-model="multiple1" />
        <label> Multiple 2 : </label>
        <input class="multiples" type="number" v-model="multiple2" />
      </div>
      <button @click="resultExo1">Submit</button>
      <div class="form__answer">
        <p>The answer is : {{ answer1 }}</p>
      </div>
    </div>

    <div class="main__exo2">
      <h2>
        By considering the terms in the Fibonacci sequence whose values do not
        exceed four million, find the sum of the even-valued terms.
      </h2>
      <div class="form__answer">
        <p>The answer is : {{ resultExo2 }}</p>
      </div>
    </div>

    <div class="main__exo3">
      <h2>
        Considering any string (or array of characters), write a program that
        identifies if the input string is a palindrome or not.
      </h2>
      <div class="form__palOrNot">
        <label> Input String : {{ palOrNot }} </label>
        <input class="multiples" type="text" v-model="palOrNot" />
      </div>
      <button @click="resultExo3">Submit</button>
      <div class="form__answer">
        <p>The answer is : {{ answer3 }}</p>
      </div>
    </div>

    <div class="main__exo4">
      <h2>
        Write a function that will accept an array of integers and sort them by
        ascending number and eliminating duplicates.
      </h2>
      <div class="form__sortArray">
        <label> Add {{ sortArray }} in the Array </label>
        <input class="multiples" type="number" v-model="sortArray" />
      </div>
      <button @click="resultExo4">Submit</button>
      <div class="form__answer">
        <p>The answer is : {{ answer4 }}</p>
      </div>
    </div>

    <div class="main__exo5">
      <h2>
        Write a function that will accept the two sorted arrays and merge them.
        Moreover, any number that appears in both arrays should be removed from
        the resulting array.
      </h2>
      <div class="form__sortArrayOne">
        <label> Add {{ addArrayOne }} in the first Array </label>
        <input class="multiples" type="number" v-model="addArrayOne" />
        <button @click="addNbArrayOne">Submit</button>
      </div>
      <div class="form__sortArrayTwo">
        <label> Add {{ addArrayTwo }} in the second Array </label>
        <input class="multiples" type="number" v-model="addArrayTwo" />
        <button @click="addNbArrayTwo">Submit</button>
      </div>
      <p>
        {{ arrayOne }}
      </p>
      <p>
        {{ arrayTwo }}
      </p>
      <button @click="resultExo5">Merge</button>
      <div class="form__answer">
        <p>The answer is : {{ answer5 }}</p>
      </div>
    </div>
  </main>
</template>

<style scoped>
.container__main {
  display: flex;
  flex-direction: column;
  gap: 50px;
}

.main__exo1,
.main__exo2,
.main__exo3,
.main__exo4,
.main__exo5 {
  display: flex;
  flex-direction: column;
  gap: 20px;
}

.form__multiples {
  display: flex;
  flex-wrap: wrap;
  gap: 20px;
}

.form__palOrNot {
  display: flex;
  flex-direction: column;
  gap: 20px;
}
</style>
