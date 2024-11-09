<script>
	import {onMount} from "svelte"
	const apiURL =
    "https://latest.currency-api.pages.dev/v1/currencies/usd.json";
  let currObject = [];
  let usd;
	let index1, index2;
	let out;

	function calc() {
		
		index1 = Number(usd[document.getElementById("curr_frm").value]);
		index2 = Number(usd[document.getElementById("curr_to").value]);
		out = (index2 / index1) * Number(document.getElementById("val").value);
		document.getElementById("output").innerHTML = out + " " + document.getElementById("curr_to").value.toUpperCase();
	}

	onMount(async () => {
    const response = await fetch(apiURL);
    if (response.status === 200) {
      console.log("Success");
      currObject = await response.json();
	    usd = currObject.usd;
			
      //   console.log(recordsObject);
      console.log(usd);
    } else {
      throw new Error(response.status);
    }
  });
	
</script>


<label for = "curr_frm">Convert from:</label>
<select name="curr_frm" id="curr_frm" on:input={calc}>
  <option value="usd" selected>USD</option>
	<option value="inr">INR</option>
  <option value="bhd">BHD</option>
  <option value="eur">EUR</option>
  <option value="aed">AED</option>
</select>

<input placeholder = "Amount" type="number" id="val" name="val" on:change={calc}>
<label for = "curr_to">Convert to:</label>
<select name="curr_to" id="curr_to" on:input={calc}>
  <option value="inr" selected>INR</option>
  <option value="bhd">BHD</option>
  <option value="eur">EUR</option>
  <option value="aed">AED</option>
</select>
<br>
<br>
<label for = "output">Converted Value: </label>
<div name = "output" id = "output">
	
</div>

