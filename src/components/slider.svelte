<script>
  import { onMount } from "svelte";

  let tempSliderValue = 0;
  let tempSliderValue2 = 0;
 

  let range;
  let range2;

  let downPayment = 0;

  function calculateDownPayment(creditScore, loanAmount) {

     // Scale the credit score to fit the desired range
    const scaledCreditScore = creditScore / 10;

    // Define a base down payment rate and calculate the down payment amount
    const baseDownPaymentRate = 0.1;  // Adjust this as needed
    // const downPaymentRate = baseDownPaymentRate + (scaledCreditScore / 100);
    let downPaymentRate = 1 / (creditScore * 0.01) - 0.1;

// Constrain the result between 0.1 and 0.25
downPaymentRate = Math.max(0.05, Math.min(0.3, downPaymentRate));

console.log(downPaymentRate);


    // Calculate and return the down payment amount
    downPayment = Math.round(loanAmount * downPaymentRate);
 }
  
  onMount(() => {
    //   range = document.getElementById("range");
  });

  function handleInput(event) {
    tempSliderValue = event.target.value;


    range = event.target;
    const progress = (tempSliderValue / range.max) * 100;
    range.style.background = `linear-gradient(to right, #f50 ${progress}%, #ccc ${progress}%)`;

    calculateDownPayment(tempSliderValue, tempSliderValue2);
  }


  function handleInput2(event) {
    tempSliderValue2 = event.target.value;


    range2 = event.target;
    const progress2 = ((tempSliderValue2)/ range2.max) * 100;
    range2.style.background = `linear-gradient(to right, #f50 ${progress2}%, #ccc ${progress2}%)`;
    calculateDownPayment(tempSliderValue,   tempSliderValue2);

  }
</script>

<div class="flex-col">
    <style>
        input[type="range"] {
          /* removing default appearance */
          -webkit-appearance: none;
          appearance: none;
          /* creating a custom design */
          width: 100%;
          cursor: pointer;
          outline: none;
          border-radius: 15px;
          /*  overflow: hidden;  remove this line*/
      
          /* New additions */
          height: 6px;
          background: #ccc;
        }
      
        /* Thumb: webkit */
        input[type="range"]::-webkit-slider-thumb {
          /* removing default appearance */
          -webkit-appearance: none;
          appearance: none;
          /* creating a custom design */
          height: 15px;
          width: 15px;
          background-color: #e22e34;
          border-radius: 50%;
          border: none;
      
          /* box-shadow: -407px 0 0 400px #f50; emove this line */
          transition: 0.2s ease-in-out;
        }
      
        /* Thumb: Firefox */
        input[type="range"]::-moz-range-thumb {
          height: 15px;
          width: 15px;
          background-color: #f50;
          border-radius: 50%;
          border: none;
      
          /* box-shadow: -407px 0 0 400px #f50; emove this line */
          transition: 0.2s ease-in-out;
        }
      
        /* Hover, active & focus Thumb: Webkit */
      
        input[type="range"]::-webkit-slider-thumb:hover {
          box-shadow: 0 0 0 10px rgba(255, 85, 0, 0.1);
        }
        input[type="range"]:active::-webkit-slider-thumb {
          box-shadow: 0 0 0 13px rgba(255, 85, 0, 0.2);
        }
        input[type="range"]:focus::-webkit-slider-thumb {
          box-shadow: 0 0 0 13px rgba(255, 85, 0, 0.2);
        }
      
        /* Hover, active & focus Thumb: Firfox */
      
        input[type="range"]::-moz-range-thumb:hover {
          box-shadow: 0 0 0 10px rgba(255, 85, 0, 0.1);
        }
        input[type="range"]:active::-moz-range-thumb {
          box-shadow: 0 0 0 13px rgba(255, 85, 0, 0.2);
        }
        input[type="range"]:focus::-moz-range-thumb {
          box-shadow: 0 0 0 13px rgba(255, 85, 0, 0.2);
        }
      
        /*=============
      Aesthetics 
      =========================*/
      
      
      
      
      </style>
      
  <div>
    <h2>What is your Credit Score</h2>
    <div class="range" style=" display: flex;
    align-items: center;
    gap: 1rem;
    max-width: 500px;
    margin: 0 auto;
    height: 4rem;
    width: 80%;
    background: #fff;
    padding: 0px 10px;">
      <input
        type="range"
        bind:value={tempSliderValue}
        min="0"
        max="800"
        id="range"
        on:input={handleInput}
      />
      <div class="value" style=" font-size: 26px;
      width: 50px;
      text-align: center;">{tempSliderValue}</div>
      
    </div>
    <div>
        <h2>The Price of you Roof</h2>
        <div class="range" style=" display: flex;
        align-items: center;
        gap: 1rem;
        max-width: 500px;
        margin: 0 auto;
        height: 4rem;
        width: 80%;
        background: #fff;
        padding: 0px 10px;">
            <input
              type="range"
              bind:value={tempSliderValue2}
              min="0"
              max="20000"
              id="range2"
              on:input={handleInput2}
            />
            <div class="value" style=" font-size: 26px;
            width: 50px;
            text-align: center;">{tempSliderValue2}</div>
            
          </div>
    </div>
  </div>
  <div class="text-4xl font-bold">
    You would have to put {downPayment} down
  </div>
</div>

