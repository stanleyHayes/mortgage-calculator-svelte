<script>
    let formatter = new Intl.NumberFormat('en-GH', {style: 'currency', currency: 'GHS'});
    let years = 15;
    let loanAmount = 200000;
    let rate = 200;
    $:yearPlural = years === 1 ? 'year' : 'years';
    $:interestRate = rate / 100;
    $:totalPayments = years * 12;
    $:montlyInterestRate = interestRate / 100 / 12;
    $:monthlyPayment =
        (loanAmount *
        Math.pow(1 + montlyInterestRate, totalPayments) * montlyInterestRate) /
        (Math.pow(1 + montlyInterestRate, totalPayments) - 1);
    $:totalPaid = monthlyPayment * totalPayments;
    $:interestPaid = totalPaid - loanAmount;
</script>

<main class="container">
    <div class="row">
        <h1>Mortgage Calculator</h1>
    </div>
    <div class="row">
        <label for="loan">Loan Amount</label>
        <input id="loan" bind:value={loanAmount} type="number" min="1" class="u-full-width" placeholder="Enter loan amount">
    </div>
    <div class="row">
        <div class="columns six">
            <label for="years">Years</label>
            <input bind:value={years} min="1" max="2000" id="years" type="range" name="years" class="u-full-width">
        </div>
        <div class="columns six outputs">
            {years} {yearPlural}
        </div>
    </div>
    <div class="row">
        <div class="columns six">
            <label for="rate">Interest Rate</label>
            <input bind:value={rate} min="1" max="2000" id="rate" type="range" name="rate" class="u-full-width">
        </div>
        <div class="columns six outputs">
            {interestRate.toFixed(2)} %
        </div>
    </div>
    <div class="row outputs">Monthly Payments {formatter.format(monthlyPayment)}</div>
    <div class="row outputs">Total Paid {formatter.format(totalPaid)}</div>
    <div class="row outputs">Interest Paid {formatter.format(interestPaid)}</div>
</main>

<style>
    .outputs {
        font-size: 20px;
        border: solid black 2px;
        margin-top: 15px;
        text-align: center;
    }
</style>