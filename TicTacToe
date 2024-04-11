const Board = ({ squares, onClick }) => (
  <div style={{
    display: 'grid',
    gridTemplateColumns: 'repeat(3, 33%)', // Fixed size for columns
    gridTemplateRows: 'repeat(3, minmax(100px, 33%))', // Use minmax for minimum height
    gap: '5px', // Use gap to simulate the borders
    backgroundColor: '#000', // Background color for the gap (border simulation)
    padding: '5px', // Padding to offset the outer gap
    minHeight: '300px', // Minimum height for the grid
    maxWidth: '100%', // Ensure the grid does not overflow its container
    margin: 'auto', // Center the grid horizontally
  }}>
    {squares.map((square, i) => (
      <Square key={i} value={square} onClick={() => onClick(i)} />
    ))}
  </div>
);

const Square = ({ value, onClick }) => (
  <button style={{
    width: '100%',
    height: '100%',
    backgroundColor: '#fff', // Background color of the square
    color: value === 'X' ? 'red' : 'blue',
    fontSize: '48px',
    display: 'flex',
    justifyContent: 'center',
    alignItems: 'center',
    border: 'none', // No border
    outline: 'none', // No outline for focus state
    boxShadow: '0 0 0 2px #000', // Simulate gap with box shadow
    margin: '-2px', // Negative margin to pull squares together and show the "gap"
  }} onClick={onClick}>
    {value}
  </button>
);

const Celebration = ({ winner }) => (
  <div style={{
    display: 'flex',
    justifyContent: 'center',
    alignItems: 'center',
    position: 'absolute',
    top: 0,
    left: 0,
    width: '100%',
    height: '100%',
    backgroundColor: 'rgba(255, 255, 255, 0.85)', // Semi-transparent white background
    color: winner === 'X' ? 'red' : 'blue',
    fontSize: '64px',
    //zIndex: 1000, // Ensure it's above everything else
  }}>
    <div className={`animate__animated animate__zoomIn`}>
      {winner} wins!
    </div>
  </div>
);


const TicTacToe = () => {
  const [squares, setSquares] = React.useState(Array(9).fill(null));
  const [xIsNext, setXIsNext] = React.useState(true);
  const winner = calculateWinner(squares);
  const [scores, setScores] = React.useState({ xWins: 0, oWins: 0, draws: 0 });

  React.useEffect(() => {
    if (winner) {
      setScores(scores => ({
        ...scores,
        xWins: winner === 'X' ? scores.xWins + 1 : scores.xWins,
        oWins: winner === 'O' ? scores.oWins + 1 : scores.oWins,
      }));
    } else if (!winner && squares.every(Boolean)) {
      setScores(scores => ({ ...scores, draws: scores.draws + 1 }));
    }
  }, [winner, squares]);

  const handleClick = (i) => {
    if (winner || squares[i]) return;
    squares[i] = xIsNext ? 'X' : 'O';
    setSquares(squares.slice());
    setXIsNext(!xIsNext);
  };

  const restartGame = () => {
    setSquares(Array(9).fill(null));
    setXIsNext(true);
  };

  const resetScores = () => {
    setScores({ xWins: 0, oWins: 0, draws: 0 });
  };

  return (
    <div style={{ position: 'relative', marginTop: '20px', textAlign: 'center' }}>
      <div>Scoreboard</div>
      <div>X Wins: {scores.xWins}</div>
      <div>O Wins: {scores.oWins}</div>
      <div>Draws: {scores.draws}</div>
      <button onClick={resetScores} style={{ marginBottom: '20px' }}>Reset Scores</button>
      <Board squares={squares} onClick={handleClick} />
      {winner && <Celebration winner={winner} />}
      {(winner || squares.every(Boolean)) && (
        <div style={{ marginTop: '20px', zIndex: '1000', position: 'inherit' }}>
          <button onClick={restartGame}>New Game</button>
        </div>
      )}
    </div>
  );
};

function calculateWinner(squares) {
  const lines = [
    [0, 1, 2],
    [3, 4, 5],
    [6, 7, 8],
    [0, 3, 6],
    [1, 4, 7],
    [2, 5, 8],
    [0, 4, 8],
    [2, 4, 6],
  ];
  for (let i = 0; i < lines.length; i++) {
    const [a, b, c] = lines[i];
    if (squares[a] && squares[a] === squares[b] && squares[a] === squares[c]) {
      return squares[a];
    }
  }
  return null;
}

// Use ReactDOM to render the TicTacToe component into the DOM
const root = ReactDOM.createRoot(document.getElementById('root'));
root.render(<TicTacToe />);
