<!DOCTYPE html>
<html lang="de">
<head>
<meta charset="UTF-8" />
<meta name="viewport" content="width=device-width, initial-scale=1" />
<title>Panfire Chess</title>
<style>
  body {
    margin: 0; background: #1e1e27; color: #eee; font-family: sans-serif;
    user-select: none;
    -webkit-user-select: none;
  }
  #game {
    position: relative;
    margin: 20px auto;
    width: 960px; height: 880px;
    background: #1e1e27;
  }
  canvas {
    background: #d7d7ba;
    display: block;
    margin: 0 auto;
  }
  #panel {
    position: absolute;
    right: 20px; top: 40px;
    width: 140px; height: 200px;
    background: #32333d;
    border-radius: 8px;
    padding: 10px;
    box-sizing: border-box;
  }
  #detonateBtn {
    background: #4682b4;
    color: white;
    border: none;
    width: 100%;
    padding: 10px;
    font-size: 16px;
    border-radius: 6px;
    cursor: pointer;
    margin-bottom: 10px;
  }
  #detonateBtn:hover {
    background: #5a9bd8;
  }
  #turnDisplay {
    font-size: 18px;
    margin-top: 10px;
    text-align: center;
  }
  #promotionDialog {
    position: fixed;
    top: 50%; left: 50%;
    transform: translate(-50%, -50%);
    background: #2a2a3a;
    padding: 20px;
    border-radius: 10px;
    display: none;
    text-align: center;
    color: white;
  }
  #promotionDialog button {
    font-size: 20px;
    margin: 5px;
    padding: 8px 14px;
    cursor: pointer;
    background: #555;
    color: white;
    border: none;
    border-radius: 6px;
    width: 45px;
  }
  #promotionDialog button:hover {
    background: #77aaff;
  }
</style>
</head>
<body>

<div id="game">
  <canvas id="board" width="880" height="880"></canvas>
  <div id="panel">
    <button id="detonateBtn" title="Detonate Pan (X)">Detonate (X)</button>
    <div id="turnDisplay">Turn: White</div>
  </div>
</div>

<div id="promotionDialog">
  <div>Promote to:</div>
  <button data-piece="Q">♕</button>
  <button data-piece="R">♖</button>
  <button data-piece="B">♗</button>
  <button data-piece="N">♘</button>
</div>

<script>
(() => {
  const BOARD_SIZE = 10;
  const CANVAS_SIZE = 880;
  const SQUARE_SIZE = CANVAS_SIZE / BOARD_SIZE;
  const LIGHT = '#f5f5dc';
  const DARK = '#78644a';
  const SELECT = '#50aae1';
  const HIGHLIGHT = '#c8e67c';
  const BG = '#1e1e27';

  const SYMBOLS = {
    'Kw': '♔', 'Qw': '♕', 'Rw': '♖', 'Bw': '♗', 'Nw': '♘', 'Pw': '♙', 'Xw': '☀',
    'Kb': '♚', 'Qb': '♛', 'Rb': '♜', 'Bb': '♝', 'Nb': '♞', 'Pb': '♟', 'Xb': '☼',
  };

  class Piece {
    constructor(kind, color) {
      this.kind = kind;
      this.color = color;
    }
  }

  class Board {
    constructor() {
      this.grid = Array(BOARD_SIZE).fill(null).map(() => Array(BOARD_SIZE).fill(null));
      this.setup();
    }
    setup() {
      // Set pieces in starting positions
      const order = ['R','X','N','B','Q','K','B','N','X','R'];
      for (let x=0; x<BOARD_SIZE; x++) {
        this.grid[0][x] = new Piece(order[x], 'w');
        this.grid[1][x] = new Piece('P', 'w');
        this.grid[9][x] = new Piece(order[x], 'b');
        this.grid[8][x] = new Piece('P', 'b');
      }
    }
    inside(x,y) {
      return x >=0 && x < BOARD_SIZE && y >=0 && y < BOARD_SIZE;
    }
    get(x,y) {
      if (!this.inside(x,y)) return null;
      return this.grid[y][x];
    }
    set(x,y,piece) {
      if (!this.inside(x,y)) return;
      this.grid[y][x] = piece;
    }
    copy() {
      let b = new Board();
      for(let y=0; y<BOARD_SIZE; y++) {
        for(let x=0; x<BOARD_SIZE; x++) {
          let p = this.get(x,y);
          if (p) b.set(x,y,new Piece(p.kind,p.color));
          else b.set(x,y,null);
        }
      }
      return b;
    }
    findKing(color) {
      for(let y=0; y<BOARD_SIZE; y++) {
        for(let x=0; x<BOARD_SIZE; x++) {
          let p = this.get(x,y);
          if (p && p.kind === 'K' && p.color === color) return [x,y];
        }
      }
      return null;
    }
    attackedSquares(color) {
      let attacks = new Set();
      for(let y=0; y<BOARD_SIZE; y++) {
        for(let x=0; x<BOARD_SIZE; x++) {
          let p = this.get(x,y);
          if (p && p.color === color) {
            for(let sq of legalMovesFrom(this,x,y,true)) {
              attacks.add(sq.toString());
            }
          }
        }
      }
      return attacks;
    }
  }

  function legalMovesFrom(board,x,y,attacksOnly=false) {
    let p = board.get(x,y);
    if (!p) return [];
    let moves = [];
    let color = p.color;
    let dirFwd = color === 'w' ? 1 : -1;
    if (p.kind === 'P' || p.kind === 'X') {
      // Pawn or Pan moves
      let ny = y + dirFwd;
      if (!attacksOnly && board.inside(x,ny) && !board.get(x,ny)) {
        moves.push([x,ny]);
        let startRank = color === 'w' ? 1 : BOARD_SIZE-2;
        if (y === startRank && !board.get(x, ny+dirFwd)) {
          moves.push([x, ny+dirFwd]);
        }
      }
      for(let dx of [-1,1]) {
        let nx = x+dx;
        let ny2 = y+dirFwd;
        if (board.inside(nx,ny2)) {
          let target = board.get(nx,ny2);
          if (attacksOnly || (target && target.color !== color)) {
            moves.push([nx, ny2]);
          }
        }
      }
    } else if (p.kind === 'N') {
      for(let [dx,dy] of [[1,2],[2,1],[-1,2],[-2,1],[1,-2],[2,-1],[-1,-2],[-2,-1]]) {
        let nx = x+dx, ny = y+dy;
        if (board.inside(nx,ny)) {
          let t = board.get(nx,ny);
          if (attacksOnly || !t || t.color !== color) {
            moves.push([nx,ny]);
          }
        }
      }
    } else if (['B','R','Q'].includes(p.kind)) {
      let directions = [];
      if (['B','Q'].includes(p.kind)) directions.push([1,1],[1,-1],[-1,1],[-1,-1]);
      if (['R','Q'].includes(p.kind)) directions.push([1,0],[-1,0],[0,1],[0,-1]);
      for(let [dx,dy] of directions) {
        let nx = x+dx, ny = y+dy;
        while(board.inside(nx,ny)) {
          let t = board.get(nx,ny);
          moves.push([nx,ny]);
          if(t) break;
          nx += dx; ny += dy;
        }
      }
    } else if (p.kind === 'K') {
      for(let dx=-1; dx<=1; dx++) {
        for(let dy=-1; dy<=1; dy++) {
          if (dx ===0 && dy===0) continue;
          let nx = x+dx, ny = y+dy;
          if (board.inside(nx,ny)) {
            let t = board.get(nx,ny);
            if (attacksOnly || !t || t.color !== color) moves.push([nx,ny]);
          }
        }
      }
    }
    return moves;
  }

  function detonateAt(board,x,y) {
    let center = board.get(x,y);
    if (!center || center.kind !== 'X') return;
    for(let dx=-1; dx<=1; dx++) {
      for(let dy=-1; dy<=1; dy++) {
        let nx = x+dx, ny = y+dy;
        if (!board.inside(nx,ny)) continue;
        if (nx === x && ny === y) continue;
        let t = board.get(nx, ny);
        if (t && t.kind !== 'K') board.set(nx, ny, null);
      }
    }
    board.set(x,y,null);
  }

  function inCheck(board,color) {
    let kingPos = board.findKing(color);
    if (!kingPos) return true;
    let [kx, ky] = kingPos;
    let enemy = color === 'w' ? 'b' : 'w';
    let attacks = board.attackedSquares(enemy);
    return attacks.has([kx,ky].toString());
  }

  function allLegalMoves(board,color) {
    let moves = [];
    for(let y=0; y<BOARD_SIZE; y++) {
      for(let x=0; x<BOARD_SIZE; x++) {
        let p = board.get(x,y);
        if (p && p.color === color) {
          for(let [nx,ny] of legalMovesFrom(board,x,y)) {
            let nb = board.copy();
            nb.set(x,y,null);
            nb.set(nx,ny,p);
            if (!inCheck(nb,color)) moves.push([x,y,nx,ny,null]);
          }
          if (p.kind === 'X') {
            let nb = board.copy();
            detonateAt(nb,x,y);
            if (!inCheck(nb,color)) moves.push([x,y,x,y,'detonate']);
          }
        }
      }
    }
    return moves;
  }

  // Setup canvas and drawing

  const canvas = document.getElementById('board');
  const ctx = canvas.getContext('2d');

  let currentBoard = new Board();
  let turn = 'w';

  let selected = null;
  let legalMovesForSelected = [];
  let dragging = false;
  let dragPos = null;

  function drawBoard() {
    ctx.clearRect(0,0,CANVAS_SIZE,CANVAS_SIZE);
    for(let y=0; y<BOARD_SIZE; y++) {
      for(let x=0; x<BOARD_SIZE; x++) {
        let lightSquare = (x+y) % 2 === 0;
        ctx.fillStyle = lightSquare ? LIGHT : DARK;
        ctx.fillRect(x*SQUARE_SIZE, (BOARD_SIZE-1 - y)*SQUARE_SIZE, SQUARE_SIZE, SQUARE_SIZE);
      }
    }
    // Highlight legal moves
    ctx.strokeStyle = HIGHLIGHT;
    ctx.lineWidth = 3;
    for(let [lx,ly] of legalMovesForSelected) {
      let rx = lx * SQUARE_SIZE + SQUARE_SIZE/2;
      let ry = (BOARD_SIZE-1 - ly)*SQUARE_SIZE + SQUARE_SIZE/2;
      ctx.beginPath();
      ctx.arc(rx, ry, SQUARE_SIZE/4, 0, Math.PI*2);
      ctx.stroke();
    }
    // Highlight selected square
    if(selected) {
      ctx.strokeStyle = SELECT;
      ctx.lineWidth = 4;
      ctx.strokeRect(selected[0]*SQUARE_SIZE, (BOARD_SIZE-1 - selected[1])*SQUARE_SIZE, SQUARE_SIZE, SQUARE_SIZE);
    }
    // Draw pieces
    for(let y=0; y<BOARD_SIZE; y++) {
      for(let x=0; x<BOARD_SIZE; x++) {
        if(selected && dragging && selected[0] === x && selected[1] === y) continue;
        let p = currentBoard.get(x,y);
        if (p) {
          let symbol = SYMBOLS[p.kind + p.color];
          ctx.fillStyle = p.color === 'w' ? '#000' : '#fff';
          ctx.font = `${SQUARE_SIZE * 0.8}px serif`;
          ctx.textAlign = 'center';
          ctx.textBaseline = 'middle';
          ctx.fillText(symbol, x*SQUARE_SIZE + SQUARE_SIZE/2, (BOARD_SIZE-1 - y)*SQUARE_SIZE + SQUARE_SIZE/2);
        }
      }
    }
    // Draw dragging piece
    if(selected && dragging && dragPos) {
      let p = currentBoard.get(selected[0], selected[1]);
      if(p) {
        let symbol = SYMBOLS[p.kind + p.color];
        ctx.fillStyle = p.color === 'w' ? '#000' : '#fff';
        ctx.font = `${SQUARE_SIZE * 0.8}px serif`;
        ctx.textAlign = 'center';
        ctx.textBaseline = 'middle';
        ctx.fillText(symbol, dragPos.x, dragPos.y);
      }
    }
  }

  function coordFromMouse(pos) {
    let rect = canvas.getBoundingClientRect();
    let mx = pos.clientX - rect.left;
    let my = pos.clientY - rect.top;
    if (mx < 0 || mx > CANVAS_SIZE || my < 0 || my > CANVAS_SIZE) return null;
    let x = Math.floor(mx / SQUARE_SIZE);
    let y = BOARD_SIZE - 1 - Math.floor(my / SQUARE_SIZE);
    return [x,y];
  }

  function makeMove(move) {
    let [fx, fy, tx, ty, special] = move;
    let p = currentBoard.get(fx, fy);
    if (!p) return;

    if (special === 'detonate') {
      detonateAt(currentBoard, fx, fy);
    } else {
      currentBoard.set(fx, fy, null);
      currentBoard.set(tx, ty, p);

      // Promotion for Pawn or Pan (X)
      if ((p.kind === 'P' || p.kind === 'X')) {
        let lastRank = p.color === 'w' ? BOARD_SIZE-1 : 0;
        if (ty === lastRank) {
          showPromotionDialog(p.color, tx, ty);
          return; // wait for promotion selection
        }
      }
    }
    turn = turn === 'w' ? 'b' : 'w';
    selected = null;
    legalMovesForSelected = [];
    dragging = false;
    dragPos = null;
    updateTurnDisplay();
    drawBoard();
  }

  function updateTurnDisplay() {
    const turnDiv = document.getElementById('turnDisplay');
    turnDiv.textContent = `Turn: ${turn === 'w' ? 'White' : 'Black'}`;
  }

  function showPromotionDialog(color, x, y) {
    promotionDialog.style.display = 'block';
    promotionDialog.dataset.color = color;
    promotionDialog.dataset.x = x;
    promotionDialog.dataset.y = y;
  }

  function hidePromotionDialog() {
    promotionDialog.style.display = 'none';
    promotionDialog.dataset.color = '';
    promotionDialog.dataset.x = '';
    promotionDialog.dataset.y = '';
  }

  function promote(pieceKind) {
    let color = promotionDialog.dataset.color;
    let x = Number(promotionDialog.dataset.x);
    let y = Number(promotionDialog.dataset.y);
    currentBoard.set(x,y,new Piece(pieceKind, color));
    hidePromotionDialog();
    turn = turn === 'w' ? 'b' : 'w';
    selected = null;
    legalMovesForSelected = [];
    dragging = false;
    dragPos = null;
    updateTurnDisplay();
    drawBoard();
  }

  canvas.addEventListener('mousedown', e => {
    if (promotionDialog.style.display === 'block') return;
    let coord = coordFromMouse(e);
    if (!coord) return;
    let [x,y] = coord;
    let p = currentBoard.get(x,y);
    if (p && p.color === turn) {
      selected = [x,y];
      legalMovesForSelected = legalMovesFrom(currentBoard, x, y);
      dragging = true;
      dragPos = {x: e.clientX, y: e.clientY};
      drawBoard();
    }
  });

  canvas.addEventListener('mousemove', e => {
    if (dragging) {
      dragPos = {x: e.clientX, y: e.clientY};
      drawBoard();
    }
  });

  canvas.addEventListener('mouseup', e => {
    if (!dragging) return;
    let coord = coordFromMouse(e);
    if (!coord) {
      // Released outside board, cancel
      selected = null;
      legalMovesForSelected = [];
      dragging = false;
      dragPos = null;
      drawBoard();
      return;
    }
    let [tx, ty] = coord;
    let [fx, fy] = selected;
    let legalAll = allLegalMoves(currentBoard, turn);
    let found = null;
    for (let m of legalAll) {
      if (m[0] === fx && m[1] === fy && m[2] === tx && m[3] === ty) {
        found = m;
        break;
