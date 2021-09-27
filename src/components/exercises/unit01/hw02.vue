<template>
  <div class="container">
    <div id="result">{{current || 0}}</div>
    <div class="calculate">
      <table>
        <tr>
          <td>
            <button class="btn first-row" @click="clean">AC</button>
          </td>
          <td>
            <button class="btn first-row" @click="undo">Del</button>
          </td>
          <td>
            <button class="btn first-row" @click="percent" value="%">%</button>
          </td>
          <td>
            <button @click="append('/')" class="btn last-col" value="/">/</button>
          </td>
        </tr>
        <tr>
          <td>
            <button @click="append('7')" class="btn" value="7">7</button>
          </td>
          <td>
            <button @click="append('8')" class="btn" value="8">8</button>
          </td>
          <td>
            <button @click="append('9')" class="btn" value="9">9</button>
          </td>
          <td>
            <button @click="append('*')" class="btn last-col" value="*">*</button>
          </td>
        </tr>
        <tr>
          <td>
            <button @click="append('4')" class="btn" value="4">4</button>
          </td>
          <td>
            <button @click="append('5')" class="btn" value="5">5</button>
          </td>
          <td>
            <button @click="append('6')" class="btn" value="6">6</button>
          </td>
          <td>
            <button @click="append('-')" class="btn last-col" value="-">-</button>
          </td>
        </tr>
        <tr>
          <td>
            <button @click="append('1')" class="btn" value="1">1</button>
          </td>
          <td>
            <button @click="append('2')" class="btn" value="2">2</button>
          </td>
          <td>
            <button @click="append('3')" class="btn" value="3">3</button>
          </td>
          <td>
            <button @click="append('+')" class="btn last-col" value="+">+</button>
          </td>
        </tr>
        <tr>
          <td colspan="2">
            <button @click="append('0')" class="btn number0" value="0">0</button>
          </td>
          <td>
            <button @click="append('.')" class="btn" value=".">.</button>
          </td>
          <td>
            <button class="btn last-col" @click="equal">=</button>
          </td>
        </tr>
      </table>
    </div>
  </div>
</template>

<script>
export default {
  data(){
    return {
      current: '',
      operations: ['%', '/', '*', '-', '+', '.'],
    }
  },
  methods: {
    clean() {
      this.current = ''
    },
    undo() {
        this.current = this.current.substring(0, this.current.length - 1)
    },
    append(number) {
      if (this.current != 'Biểu thức lỗi') {
        let current = this.current
        let flagOperation = false
        let flagChar = false
        this.operations.forEach((value) => {
          if (number == value) {
            flagOperation = true
          }
          if (current.charAt(current.length - 1) == value) {
            flagChar = true
          }
        })
        if (current.length == 1 && current.charAt(0) === '0') {
          if (flagOperation) {
            this.current += number
          } else {
            this.current = number
          }
        } else if (flagOperation && flagChar) {
          this.current = this.current.slice(0, -1) + number
        }
        else if (current.length > 1 && flagChar) {
          if (!flagOperation) {
            this.current += number
          }
        } else {
          this.current += number
        }
      }
    },
    equal() {
      if (this.current != 'Biểu thức lỗi') {
        let flagEqual = true
        this.operations.forEach((value) => {
          if (this.current.charAt(this.current.length-1) == value) {
            flagEqual = false
          }
        })
        if (flagEqual) {
          this.current = String(eval(this.current))
          if (this.current == 'NaN') {
            this.current = 'Biểu thức lỗi'
          }
        }
      }
    },
    percent() {
      if (this.current != 'Biểu thức lỗi') {
        let flagPercent = -1
        let check = false
        let lastNumber = ''
        let current = this.current
        for (let i = 0; i < current.length; i++){
          this.operations.forEach((value) => {
            if (current[i] == value){
              flagPercent = i
            }
            if (current.charAt(current.length - 1) == value){
              check = true
            }
          })
        }
        if (flagPercent != -1) {
          if (!check) {
            lastNumber = current.slice(flagPercent + 1, current.length)
            lastNumber = String(lastNumber / 100)
            this.current = current.slice(0, flagPercent + 1) + lastNumber
          }
        } else {
          lastNumber = current.slice(0, current.length)
          lastNumber = String(lastNumber / 100)
          this.current = lastNumber
        }
      }
    },
  }
}
</script>
<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
  @import "src/assets/scss/Unit01/hw02";
</style>
