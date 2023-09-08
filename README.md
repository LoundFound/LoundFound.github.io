# LoundFound.github.io
<!DOCTYPE html>
<html>
  <head>
    <meta http-equiv="Content-Type" content="text/html;charset=utf-8">
    <title>First WebGL Demo</title>
    <!-- 顶点着色器和片元着色器代码 -->
    <script id="vertex-shader" type="x-shader/x-vertex">
      attribute vec4 vPosition;
      void main(){
        gl_Position = vPosition;
      }
    </script>
    <script id="fragment-shader" type="x-shader/x-fragment">
      precision mediump float;
      void main(){
        gl_FragColor = vec4( 1.0, 0.0, 0.0, 1.0 );
      }
    </script>
    <!-- 一组相关的JS库 -->
    <script type="text/javascript" src="js/common/webgl-utils.js"></script>
    <script type="text/javascript" src="js/common/initShaders.js"></script>
    <script type="text/javascript" src="js/common/glMatrix-0.9.5.min.js"></script>
    <!-- 绘制三角形的JS代码 -->
    <script type="text/javascript" src="js/triangle.js"></script>
  </head>
  <body>
    <canvas id="triangle-canvas" style="border:none;" width="500" height="500"></canvas>
  </body>
</html>
认识WEBGL程序
JAVASCRIPT SOURCE
"use strict";
 
var gl;
var points;
 
window.onload = function init(){
  var canvas = document.getElementById( "triangle-canvas" );
  gl = WebGLUtils.setupWebGL( canvas );
  if( !gl ){
    alert( "WebGL isn't available" );
  }
 
  // Three Vertices
  var vertices = [
     -0.5, -0.5,
     0.0, 0.5,
     0.5, -0.5
  ];
 
  // Configure WebGL
  gl.viewport( 0, 0, canvas.width, canvas.height );
  gl.clearColor( 0.0, 0.0, 0.0, 1.0 );
 
  // Load shaders and initialize attribute buffers
  var program = initShaders( gl, "vertex-shader", "fragment-shader" );
  gl.useProgram( program );
 
  // Load the data into the GPU
  var bufferId = gl.createBuffer();
  gl.bindBuffer( gl.ARRAY_BUFFER, bufferId );
  gl.bufferData( gl.ARRAY_BUFFER, new Float32Array( vertices ), gl.STATIC_DRAW );
 
  // Associate external shader variables with data buffer
  var vPosition = gl.getAttribLocation( program, "vPosition" );
  gl.vertexAttribPointer( vPosition, 2, gl.FLOAT, false, 0, 0 );
  gl.enableVertexAttribArray( vPosition );
  render();
}
 
function render(){
  gl.clear( gl.COLOR_BUFFER_BIT );
  //gl.drawArrays( gl.TRIANGLE_FAN, 0, 4 );
  gl.drawArrays( gl.TRIANGLES, 0, 3 );
  //gl.drawArrays( gl.TRIANGLE_FANS, 3, 6 );
}       
5 . 1 

