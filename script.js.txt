const canvas = document.getElementById("canvas");
const ctx = canvas.getContext("2d");

canvas.width = window.innerWidth;
canvas.height = window.innerHeight;

let points = [];
let t = 0;

function heart(t) {
  return {
    x: 16 * Math.pow(Math.sin(t), 3),
    y:
      13 * Math.cos(t) -
      5 * Math.cos(2 * t) -
      2 * Math.cos(3 * t) -
      Math.cos(4 * t),
  };
}

function draw() {
  ctx.fillStyle = "rgba(0,0,0,0.1)";
  ctx.fillRect(0, 0, canvas.width, canvas.height);

  const pos = heart(t);
  points.push({
    x: canvas.width / 2 + pos.x * 15,
    y: canvas.height / 2 - pos.y * 15,
  });

  ctx.fillStyle = "#ff3366";
  for (let p of points) {
    ctx.beginPath();
    ctx.arc(p.x, p.y, 2, 0, Math.PI * 2);
    ctx.fill();
  }

  t += 0.05;
  if (points.length > 1500) points.shift();

  requestAnimationFrame(draw);
}

draw();
