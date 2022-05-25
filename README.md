# node-tsserver
Servidor Express.js simples e minimalista feito em Typescript e uma coleção de decorators.

## Instalação

```bash
$ npm install --save @troninformatica/node-tsserver
```

e em seu tsconfig.json:

```json
{
  "module": "commonjs",
  "moduleResolution": "node",
  "target": "es5",
  "emitDecoratorMetadata": true,
  "experimentalDecorators": true,
  "lib": [
    "dom",
    "es2018"
  ],
}
```

## Como utilizar

Crie um componente ServerLoader que estende o servidor e use o decorador ServerSettings para configurar o servidor:

```javascript
import { ServerSettings, ServerLoader } from '@troninformatica/node-tsserver';

@ServerSettings({
  httpPort: 5001,
  apiPrefix: 'api',
  cors: true,
  controllersPath: 'src/controllers'
})
export class Server extends ServerLoader {

  start() {
    super.startHttpServer(); // Você pode opcionalmente passar uma função de retorno de chamada.
  }
}
```

e crie um controlador como este:

```javascript
import { Controller, Get, Post } from '@troninformatica/node-tsserver';
import { Request, Response } from 'express';

@Controller('sample')
export class SampleController {

  @Get(':id')
  getById(req: Request, res: Response) {
    res.status(200).json({ status: 'OK', id: req.params.id });
  }
  
  @Post()
  create(req: Request, res: Response) {
    res.status(200).json(req.body);
  }
}
```

Agora, basta criar uma instância do seu servidor e você está pronto para utilizar

```javascript
import { Server } from './Server';

const server = new Server():
server.start();
```

Simples assim, aproveite! xD

## Documentação

Por enquanto, os seguintes decoradores de classe estão disponíveis:
* ServerSettings
* Controller

E os decoradores de métodos:
* Get
* Post
* Put
* Patch
* Delete


Obrigado.
