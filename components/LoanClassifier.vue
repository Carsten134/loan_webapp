<script setup>
  const getsLoan = ref(false)
  const submited = ref(false)

  const age = ref(20)
  const gender = ref("female")
  const income = ref(20000)
  const emplExp = ref(0)
  const loanAmount = ref(10000)
  const loanIntRate = ref(3)
  const education = ref("High School")
  const homeOwn = ref("Rent")
  const loanIntent = ref("personal")
  const prevDefault = ref("No")
  const credLength = ref(0)

  async function submitData() {
      const {data, error} = await $fetch("https://carstenstahl.us-east-1.aws.modelbit.com/v1/predict_loan/latest", {
        method: 'POST',
        body: {data: [age.value, gender.value, income.value, emplExp.value, loanAmount.value, loanIntRate.value, education.value, homeOwn.value, loanIntent.value, prevDefault.value,
          credLength.value
        ]}
      })
      if (error) {
        console.log(error)
        return null
      }
      submited.value = true
      getsLoan.value = data[0]
      console.log("API answered with 200: ", data[0])
      // gets_loan.value = data.weather
    }
</script>

<template>
  <div class="h-screen w-screen flex flex-col justify-center items-center">
    <h1 class="font-bold text-2xl">Will you get the loan?</h1>
    <div class="w-[75%]">
      This little webapp will check if you would be classified to get a loan approved. It does so by calling a remotely stored XGB-classifier, trained on 43k rows of synthetic data.<strong>Do not insert your real data! API calls are stored on the server.</strong>
      <form class="border-solid border-[1px] shadow-sm rounded-md p-3 text-xl mt-3" onsubmit="event.preventDefault()" v-if="!submited">
        <div class="mb-2">
          <label for="test" class="mr-2">Your age</label>
          <input type="number" id="test" class="shadow-sm border-solid border-[1px] hover:border-slate-500 active:border-slate-600 active:border-[1px] transition-all ease-in-out" required v-model="age">
        </div>
        <div class="mb-2">
          <label for="gender" class="mr-2">Your gender</label>
          <select name="gender" id="gender" class="shadow-sm border-solid border-[1px] hover:border-slate-500 active:border-slate-600 active:border-[1px] transition-all ease-in-out" required v-model="gender">
            <option value="female">female</option>
            <option value="male">male</option>
          </select>
        </div>
        <div class="mb-2">
          <label for="income" class="mr-2">Your yearly income in $</label>
          <input type="number" id="income" name="income" class="shadow-sm border-solid border-[1px] hover:border-slate-500 active:border-slate-600 active:border-[1px] transition-all ease-in-out" required v-model="income">
        </div>
        <div class="mb-2">
          <label for="exp" class="mr-2">Your employment experience in years:</label>
          <input type="number" id="exp" class="shadow-sm border-solid border-[1px] hover:border-slate-500 active:border-slate-600 active:border-[1px] transition-all ease-in-out" required v-model="emplExp">
        </div>
        <div class="mb-2">
          <label for="loanAmt" class="mr-2">Your loan amount $</label>
          <input type="number" id="loanAmt" name="loanAmt" class="shadow-sm border-solid border-[1px] hover:border-slate-500 active:border-slate-600 active:border-[1px] transition-all ease-in-out" required v-model="loanAmount">
        </div>
        <div class="mb-2">
          <label for="intRate" class="mr-2">Your loan interest rate in %</label>
          <input type="number" id="intRate" name="intRate" class="shadow-sm border-solid border-[1px] hover:border-slate-500 active:border-slate-600 active:border-[1px] transition-all ease-in-out" required v-model="loanIntRate">
        </div>
        <div class="mb-2">
          <label for="education" class="mr-2">Your highest education</label>
          <select name="education" id="education" class="shadow-sm border-solid border-[1px] hover:border-slate-500 active:border-slate-600 active:border-[1px] transition-all ease-in-out" required v-model="education">
            <option value="Doctorate">Doctorate</option>
            <option value="Master">Master</option>
            <option value="Bachelor">Bachelor</option>
            <option value="High School">High School</option>
            <option value="Associate">Associate</option>
          </select>
        </div>
        <div class="mb-2">
          <label for="home" class="mr-2">Your highest home ownership status</label>
          <select name="home" id="home" class="shadow-sm border-solid border-[1px] hover:border-slate-500 active:border-slate-600 active:border-[1px] transition-all ease-in-out" required v-model="homeOwn">
            <option value="RENT">Rent</option>
            <option value="OWN">Own</option>
            <option value="MORTGAGE">Mortage</option>
            <option value="OTHER">Other</option>
          </select>
        </div>
        <div class="mb-2">
          <label for="Intent" class="mr-2">How do you intent to use the loan</label>
          <select name="Intent" id="Intent" class="shadow-sm border-solid border-[1px] hover:border-slate-500 active:border-slate-600 active:border-[1px] transition-all ease-in-out" required v-model="loanIntent">
            <option value="PERSONAL">personal</option>
            <option value="MEDICAL">medical</option>
            <option value="VENTURE">venture</option>
            <option value="HOMEIMPROVEMENT">homeimprovement</option>
            <option value="DEBTCONSOLIDATION">debt consolidation</option>
          </select>
        </div>
        <div class="mb-2">
          <label for="prevDefault" class="mr-2">Did you default on a loan before</label>
          <select name="prevDefault" id="prevDefault" class="shadow-sm border-solid border-[1px] hover:border-slate-500 active:border-slate-600 active:border-[1px] transition-all ease-in-out" required v-model="prevDefault">
            <option value="Yes">Yes</option>
            <option value="No">No</option>
          </select>
        </div>
        <div class="mb-2">
          <label for="credHist" class="mr-2">How long since you got your first loan (in years)?</label>
          <input type="number" id="credHist" name="credHist" class="shadow-sm border-solid border-[1px] hover:border-slate-500 active:border-slate-600 active:border-[1px] transition-all ease-in-out" required v-model="credLength">
        </div>
        
        
        <button class="relative bg-slate-400 text-white transition-all hover:ease-in-out px-2 py-1 text-xl rounded-full duration-700 hover:shadow-md hover:shadow-orange-500 hover:text-black hover:border-1 hover:border-solid hover:border-orange-500 hover:bg-white"
        @click="submitData">
          Submit
      </button>
      </form>
    </div>
    

    <div class="text-2xl text-green-500 font-bold w-[75%] flex flex-col justify-center" v-if="getsLoan & submited">
      <div>Congrats you will get the loan!</div>
      <img src="../server/money-rain.webp" class="rounded-md shadow-md" alt="">
    </div>
    <div class="text-2xl text-red-600 font-bold" v-if="!getsLoan & submited">You will not get the loan!</div>
    
  </div>
</template>