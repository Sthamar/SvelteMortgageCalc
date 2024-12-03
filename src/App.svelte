<script>
	var formatter = new Intl.NumberFormat("en-US",{
		style:"currency",
		currency:"USD"
	})
	let loanAmount = 200000;
	let years = 15;
	let interestRateInput = 200;
	$: interestRate = interestRateInput/100;
	$: totalPayments = years * 12; 
	$: monthlyInterestRate = interestRate / 100 / 12;
	$: monthlyPayments = (loanAmount * Math.pow(1+monthlyInterestRate, totalPayments) * monthlyInterestRate)/(Math.pow(1 + monthlyInterestRate, totalPayments)-1);
	$: totalPaid = monthlyPayments * totalPayments;
	$: interestPaid = totalPaid - loanAmount;
</script>

<style>
	.outputs{
		font-size: 20px;
		border: solid black 2px;
		margin-top: 15px;
		text-align: center;
	}
</style>

<main class="container">
	<div class="row">
		<h1>Mortgage Calculator</h1>
	</div>
	<div class="row">
		<!-- svelte-ignore a11y-label-has-associated-control -->
		<label>Loan Amount</label>
		<input type="number" min="1" class="u-full-width" placeholder="Enter loan amount" bind:value={loanAmount}>
	</div>
	<div class="row">
		<div class="columns six">
			<!-- svelte-ignore a11y-label-has-associated-control -->
			<label>Years</label>
			<input type="range" class="u-full-width" min="1" max="50" bind:value={years}>

		</div>
		<div class="columns six outputs">
			{years} years
		</div>
	</div>
	<div class="row">
		<div class="columns six">
			<!-- svelte-ignore a11y-label-has-associated-control -->
			<label>Interest Rate</label>
			<input type="range" class="u-full-width" min="1" max="2000" bind:value={interestRateInput}>

		</div>
		<div class="columns six outputs">
			{interestRate.toFixed(2)} %
		</div>
	</div>
	<div class="row outputs">Monthly Payments {formatter.format(monthlyPayments)}</div>
	<div class="row outputs">Total Paid {formatter.format(totalPaid)}</div>
	<div class="row outputs">Interest Paid {formatter.format(interestPaid)}</div>

</main>