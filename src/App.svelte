<script>
  import Button from "./Button.svelte";
  function calculate(input) {
    if (input.length === 0 || !Array.isArray(input)) return 0;
    const result = input.reduce((acc, val, idx, arr) => {
      const nextNumber = Number(arr[idx + 1]);
      if (isNaN(nextNumber)) return acc;
      switch (val) {
        case "+":
          return acc + nextNumber;
        case "-":
          return acc - nextNumber;
        case "*":
          return acc * nextNumber;
        case "/":
          return acc / nextNumber;
      }

      return acc;
    }, Number(input[0]));

    return result;
  }
  $: input = [];
  $: result = calculate(input);
  function action(value) {
    const lastIndex = input.length - 1;
    const lastInputValue = input[lastIndex];
    const isLastInputNumber = !isNaN(input[lastIndex]);
    const isValueNumber = !isNaN(value);
    if (value === "C") {
      input = [];
      finalResult = 0;
      input = [...input.slice(0, -2)];
    } else if (value === "=") {
      input = [`${result}`];
    } else if (isValueNumber && isLastInputNumber) {
      input = [...input.slice(0, -1), `${lastInputValue}${value}`];
    } else if (!isValueNumber && !isLastInputNumber) {
      input = [...input.slice(0, -1), value];
    } else {
      input = [...input, value];
    }
  }
</script>

<style>
  :global(html) {
    font-size: 10px;
  }
  :global(body) {
    display: flex;
    align-items: center;
    justify-content: center;
    padding: 0;
    font-size: 2.4rem;
    color: #393a42;
  }
  .result {
    margin-bottom: 1rem;
    text-align: top;
    width: 250px;
  }
</style>

<p class="result">{input.join(' ')}</p>
<div>
  <Button value={'C'} {action} />
  <br />
  <Button value={7} {action} />
  <Button value={8} {action} />
  <Button value={9} {action} />
  <Button value={'*'} {action} />
  <br />

  <Button value={4} {action} />
  <Button value={5} {action} />
  <Button value={6} {action} />
  <Button value={'-'} {action} />
  <br />

  <Button value={1} {action} />
  <Button value={2} {action} />
  <Button value={3} {action} />
  <Button value={'+'} {action} />
  <br />
  <Button value={'/'} {action} />
  <Button value={0} {action} />
  <Button value={'='} {action} />
</div>
