
<script>
	let fromcurr='inr';
	let tocurr='usd';
	let inval=1;
	let outval=84.48;
	let convrate=1;
	let currval={};
    async function fetchData() {
        try {
            const response = await fetch('https://latest.currency-api.pages.dev/v1/currencies/usd.json'); // Replace with your API URL
            const data = await response.json();
        if (data && data.rates) {
            currval = data.rates; // Store the conversion rates in 'currencies'
            
			
			if (fromcurr=='usd'){
				convrate=currval[tocurr];
				outval=inval*convrate;
			}
			else if (tocurr=='usd'){
				convrate=currval[tocurr];
				outval=inval/convrate;
			}
			else {
				convrate=currval[fromcurr];
				inval/=convrate
				convrate=currval[tocurr];
				outval=inval*convrate
			}
        }

        }    
		
    
        catch (error) {
            console.error("Error fetching currency rates: ", error); // Handle any errors
        }
    }
    fetchData();
    
</script>

<main>
<div>
	<p id=text>Enter the value and currency you want to convert from</p>
	<input bind:value={inval}>
	<input bind:value={fromcurr}/>
</div>
<div>
	<p id=text>Enter the currency you vant to convert to</p>
	<p style="display: inline-block;">{outval}</p>
	<input bind:value={tocurr}>
</div>
</main>

<style>

</style>