
<script>
	let fromcurr='usd';
	let tocurr='inr';
	let inval=1;
	let outval=84.48;
	let convrate=1;
	let currval={};
    async function fetchData() {
			const url=`https://latest.currency-api.pages.dev/v1/currencies/${fromcurr}.json`;
        try {
            const response = await fetch(url); // Replace with your API URL
					const data = await response.json();
            currval = data[fromcurr]; // Store the conversion rates in 'currencies'
            updateOutval();
					
			
				
					
			
			}
          
		
    
        catch (error) {
            console.error("Error fetching currency rates: ", error); // Handle any errors
        }
    }
	function updateOutval() {
		convrate=currval[tocurr];
				outval=inval*convrate;
	}
 $: fetchData(), [fromcurr, tocurr];  
	$: updateOutval(), [inval];
</script>

<main>
<div>
	<p id=text>Enter the value and currency you want to convert from</p>
	<input type="number" bind:value={inval}>
	<input type="text" bind:value={fromcurr}/>
</div>
<div>
	<p id=text>Enter the currency you vant to convert to</p>
	<p style="display: inline-block;">{outval}</p>
	<input type="text" bind:value={tocurr}>
</div>
</main>

<style>

</style>
