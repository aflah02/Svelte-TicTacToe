<script>
	let buttons = new Array(9).fill(null);
	let result = null;
	let turn = 'X';
	const winCombinations = [
		[0, 1, 2],
		[3, 4, 5],
		[6, 7, 8],
		[0, 3, 6],
		[1, 4, 7],
		[2, 5, 8],
		[0, 4, 2],
	];
	function restart() {
		buttons = new Array(9).fill(null);
		result = null;
		turn = 'X';
		console.log(result);
	}
	function setValue(i){
		if (buttons[i] != null){
			return;
		}
		buttons[i] = turn;
		buttons = [...buttons];
		turn = turn === 'X' ? 'O' : 'X';
		if (!buttons.includes(null)){
			checkWinner();
			if (result === null){
				result = 'Draw';
			}
		} else{
			checkWinner();
		}
	}
	function checkWinner(){
		for (let i=0;i<winCombinations.length;i++){
			if (buttons[winCombinations[i][0]] != null){
				if (buttons[winCombinations[i][0]] == buttons[winCombinations[i][1]] && buttons[winCombinations[i][1]] == buttons[winCombinations[i][2]]){
					result = buttons[winCombinations[i][0]] + ' wins';
					console.log(result);
					break;
				}
			}
		}
		if (buttons[0] == buttons[4] && buttons[4] == buttons[8] && buttons[0] != null){
			result = buttons[0] + ' wins';
			console.log(result);
		}
		if (buttons[2] == buttons[4] && buttons[4] == buttons[6] && buttons[2] != null){
			result = buttons[2] + ' wins';
			console.log(result);
		}
	}
	console.log(result);
</script>

<style>
	.tictac {
		place-items: center;
		width: 300px;
		height: 300px;
		display: flex;
		flex-wrap: wrap;
		text-align: center;
		margin-top: 20px;
		position: relative;
		top: 40%;
		left: 40%;
		-webkit-transform: translateY(-50%);
		-ms-transform: translateY(-50%);
		transform: translateY(-50%);
	}
	.tictac button {
		width: 100px;
		height: 100px;
		margin: 0px;
	}
	/* <!-- Center Of Page Vertically --> */
	.res {
		text-align: center;
		margin-top: 20px;
		position: relative;
		top: 50%;
		-webkit-transform: translateY(-50%);
		-ms-transform: translateY(-50%);
		transform: translateY(-50%);
	}
	.title {
		text-align: center;
	}
</style>

<h1 class="title">TicTacToe</h1>
{#if !result}
	<div class="tictac">
		{#each buttons as button, i}
			<button on:click={()=>{setValue(i)}}>
				{button?button:""}
			</button>
		{/each}
	</div>
{:else}

	<div class="res">
		{result}
		<button on:click={restart}>
			Restart
		</button>
	</div>
{/if}