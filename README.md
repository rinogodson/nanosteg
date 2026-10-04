<img width="415" height="489" alt="image" src="https://github.com/user-attachments/assets/64eceb1e-c6f5-4807-af48-3bad769362dd" />

# nanosteg

This is a tool to hide text inside text for secret communications...
and the crazy part is, this entire tool is under 3kb!

## how to use it

The Default Tab is "HIDE", where you can enter your 'Secret' text, and the 'Carrier' text (the text everyone sees) and click the 'Hide' button to generate the output, then you need to copy this output using copy button.

To show what's inside an output made like this, go to the "SHOW" tab, and paste the text you have there, and click 'Show' button to show the hidden secret inside the input text.

## how it works

This is the logic of this algorithm.
Unicode characters from 0xFF00 to 0xFE0F are 16 chars.
Characters from 0xE0100 to 0xE01EF are 240 chars.
Which means there are 256 characters, and the crazy part is that these are invisible too this tool basically converts the secret text to these characters and then append them to the carrier.

## building

```
npm install
node build.mjs
```

## usage

you can paste this into your browser to use this app:

```
data:text/html,<div id=u><h1>nanosteg</h1><div id=x><button id=hb>HIDE</button><button id=sb class=n>SHOW</button></div><div id=ht><input id=m placeholder=Secret ><input id=c placeholder=Carrier ><button id=h>Hide</button></div><div id=st hidden><input id=l placeholder=Paste ><button id=s>Show</button></div><input id=o readonly placeholder=Output ><button id=p>Copy</button><button id=r>Clear</button><style>*{outline:0}body{background:black;color:white;font-family:monospace;font-size:1rem;height:100vh;display:grid;place-items:center}%23u{width:300px;display:grid;gap:10px;background:%23444;padding:10px;place-items:center;opacity:.9}canvas{position:fixed;inset:0;pointer-events:none}input,button{background:%23222;color:white;width:100%25;padding:6px 8px;border:2px %23222 solid;font:inherit}button:active{filter:brightness(1.3)}input{background:gray;border-color:%23222}input:focus{background:%23666}%23x{display:flex}%23hb,%23sb{background:black}div{gap:10px;width:100%25}.n{opacity:.5}</style><script>let e,n,a;BC=document.createElement("canvas"),bcw=BC.width=200,BC.height=1,BC.style.cssText="filter:saturate(0);opacity:.17;position:fixed;inset:0;z-index:-1;width:100%25;height:100%25",u.before(BC),BX=BC.getContext("2d"),BD=BX.createImageData(bcw,1),D=BD.data,t=0,function e(){t+=.03,M=Math;for(let e=0;e<bcw;e++){const n=M.sin(e/9+t)+M.sin(-t)+M.sin(e/12+t)+M.sin(M.hypot(e-80,45)/6-2*t),a=4*e;D[a]=128+127*M.sin(n*M.PI),D[a+1]=128+127*M.sin(n*M.PI+2),D[a+2]=128+127*M.sin(n*M.PI+4),D[a+3]=255}BX.putImageData(BD,0,0),requestAnimationFrame(e)}(),q=()=>m.value=c.value=l.value=o.value="",R=M.random,C=document.createElement("canvas"),u.append(C),X=C.getContext("2d"),P=[],W=C.width=innerWidth,H=C.height=innerHeight,B=(e,t)=>{for(let n=30;n--;)P.push([e+30*R()-15,t+30*R()-15,10*R()-5,-10*R()-3,2*R()+1,360*R(),1])},setInterval(e=>{X.clearRect(0,0,W,H);for(let e=P.length;e--;){let t=P[e];t[0]+=t[2],t[1]+=t[3],t[3]+=.4,t[2]*=.98,t[6]-=.02,t[6]<0||t[1]>H+30?P.splice(e,1):(X.globalAlpha=t[6],X.fillStyle=`hsl(${t[5]},90%25,60%25)`,X.fillRect(t[0],t[1],t[4],2*t[4]))}},17),u.onclick=t=>{const c=t.target.tagName[0],i="B"==c?300:"I"==c?200:0;i&&(e=e||new AudioContext,n=e.createOscillator(),a=e.createGain(),n.frequency.value=i,n.connect(a).connect(e.destination),a.gain.value=.08,a.gain.exponentialRampToValueAtTime(.001,e.currentTime+.5),n.start(),n.stop(e.currentTime+.5)),"hsp".includes(t.target.id)&&B(t.clientX,t.clientY)},x.onclick=e=>{const t=e.target==hb;ht.hidden=!t,st.hidden=t,hb.className=t?"":"n",sb.className=t?"n":"",q()},encoder=new TextEncoder,decoder=new TextDecoder,h.onclick=()=>o.value=((e,t)=>{let n="";for(const e of encoder.encode(t))n+=String.fromCodePoint(e<16?65024+e:917744+e);return e+n})(c.value,m.value),s.onclick=()=>o.value=(e=>{let t=[];for(const n of e){const e=n.codePointAt(0);let a=-1;if(e>=65024&&e<65040?a=e-65024:e>=917760&&e<=917999&&(a=e-917760+16),a<0){if(t.length)break}else t.push(a)}return decoder.decode(new Uint8Array(t))})(l.value),p.onclick=()=>navigator.clipboard.writeText(o.value),r.onclick=q;</script></div>
```
