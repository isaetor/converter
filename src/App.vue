<script>
  export default {
  data() {
    return {
      mode:"dec",
      hexadecimalNumber: '',
      decimalNumber: '',
      octalNumber: '',
      binaryNumber: '',
    }
  },

  methods: {
    output(number){
      return !number ?  0 : number
    },
    convertTo() {
      
      switch (this.mode) {
        case "hex":
          this.hexadecimalNumber = this.hexadecimalNumber.replace(/[^0-9A-Fa-f]/g, '');
          const decimal = parseInt(this.hexadecimalNumber, 16);
          this.decimalNumber = decimal.toString(10);
          this.octalNumber = decimal.toString(8);
          this.binaryNumber = decimal.toString(2);
          break;
        case "dec":
          this.decimalNumber = this.decimalNumber.replace(/[^0-9]/g, '');
          this.hexadecimalNumber = parseInt(this.decimalNumber).toString(16);
          this.octalNumber = parseInt(this.decimalNumber).toString(8);
          this.binaryNumber = parseInt(this.decimalNumber).toString(2);
          break;
        case "oct":
          this.octalNumber = this.octalNumber.replace(/[^0-7]/g, '');
          this.hexadecimalNumber = parseInt(this.octalNumber, 8).toString(16);
          this.decimalNumber = parseInt(this.octalNumber, 8).toString(10);
          this.binaryNumber = parseInt(this.octalNumber, 8).toString(2);
          break;
        case "bin":
          this.binaryNumber = this.binaryNumber.replace(/[^0-1]/g, '');
          this.hexadecimalNumber = parseInt(this.binaryNumber, 2).toString(16);
          this.decimalNumber = parseInt(this.binaryNumber, 2).toString(10);
          this.octalNumber = parseInt(this.binaryNumber, 2).toString(8);
          break;
      }
      
      if(!this.hexadecimalNumber || !this.decimalNumber || !this.octalNumber || !this.binaryNumber){
        this.hexadecimalNumber = '';
        this.decimalNumber = '';
        this.octalNumber = '';
        this.binaryNumber = '';
      }
    },

  },

}
</script>

<template>
  <div class="flex items-center justify-center h-screen bg-neutral-200">
    <div class="w-80">
      <div class="relative rounded-md shadow-sm mb-4">
        <input v-if="mode == 'hex'" v-model="hexadecimalNumber" @input="convertTo" @emptied="output" type="text" autocomplete="off" name="number" class="block w-full rounded-md border border-neutral-200 py-1.5 px-3 text-gray-900 placeholder:text-gray-400 sm:text-sm sm:leading-6" placeholder="12345" />
        <input v-else-if="mode == 'dec'" v-model="decimalNumber" @input="convertTo" type="text" autocomplete="off" name="number" class="block w-full rounded-md border border-neutral-200 py-1.5 px-3 text-gray-900 placeholder:text-gray-400 sm:text-sm sm:leading-6" placeholder="12345" />
        <input v-else-if="mode == 'oct'" v-model="octalNumber" @input="convertTo" type="text" autocomplete="off" name="number" class="block w-full rounded-md border border-neutral-200 py-1.5 px-3 text-gray-900 placeholder:text-gray-400 sm:text-sm sm:leading-6" placeholder="12345" />
        <input v-else-if="mode == 'bin'" v-model="binaryNumber" @input="convertTo" type="text" autocomplete="off" name="number" class="block w-full rounded-md border border-neutral-200 py-1.5 px-3 text-gray-900 placeholder:text-gray-400 sm:text-sm sm:leading-6" placeholder="12345" />
        <div class="absolute inset-y-1 right-2 flex items-center z-10 bg-white">
          <select v-model="mode" name="currency" class="h-full rounded-md border-0 bg-transparent py-0 pl-2 pr-7 text-gray-500 sm:text-sm">
            <option value="hex">HEX</option>
            <option value="dec">DEC</option>
            <option value="oct">OCT</option>
            <option value="bin">BIN</option>
          </select>
        </div>
      </div>
      <div class="text-neutral-500">
        <p class="flex items-center gap-8 h-8"><span>HEX</span><span class="w-full overflow-x-auto scrollbar">{{output(hexadecimalNumber)}}</span></p>
        <p class="flex items-center gap-8 h-8"><span>DEC</span><span class="w-full overflow-x-auto scrollbar">{{output(decimalNumber)}}</span></p>
        <p class="flex items-center gap-8 h-8"><span>OCT</span><span class="w-full overflow-x-auto scrollbar">{{output(octalNumber)}}</span></p>
        <p class="flex items-center gap-8 h-8"><span>BIN </span><span class="w-full overflow-x-auto scrollbar">{{output(binaryNumber)}}</span></p>
      </div>
    </div>
  </div>
</template>