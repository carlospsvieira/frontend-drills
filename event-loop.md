## As 3 peças
Call stack: onde o código síncrono executa, uma função por vez. Enquanto ela não esvazia, nada mais roda.
Microtask queue: callbacks de Promise (.then, await) e queueMicrotask. Prioridade alta.
Task queue (macrotasks): setTimeout, setInterval, eventos de I/O e de clique. Prioridade menor.

## A regra do loop
Executa tudo da call stack até esvaziar.
Esvazia todas as microtasks.
Pega uma task da task queue.
Repete.

```
console.log('1');
setTimeout(() => console.log('2'), 0);
Promise.resolve().then(() => console.log('3'));
console.log('4');
>> Saída: 1, 4, 3, 2
```
1 e 4: síncronos, rodam direto na stack.
3: microtask, roda assim que a stack esvazia.
2: task, só roda depois de todas as microtasks, mesmo com delay 0.

O 0 do setTimeout não significa “agora”, significa “o mais cedo possível, depois que a stack e as microtasks terminarem”.


