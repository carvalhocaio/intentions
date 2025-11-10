# Fastify + Bun Template

A modern, high-performance REST API template using [Fastify](https://fastify.dev/)
and [Bun](https://bun.sh/). This template includes TypeScript support, automatic API
documentation, type-safe validation, and code formatting out of the box.

## Features

- **Lightning Fast**: Powered by Bun runtime and Fastify framework
- **Type-Safe**: Full TypeScript support with Zod schema validation
- **Auto Documentation**: Interactive API docs with Swagger/OpenAPI and Scalar UI
- **Schema Validation**: Request/response validation using `fastify-type-provider-zod`
- **Code Formatting**: Integrated Biome for fast linting and formatting
- **Hot Reload**: Development mode with automatic restart on file changes
- **CORS**: Pre-configured CORS support

## Prerequisites

- [Bun](https://bun.sh/) >= 1.0.0

## Getting Started

### 1. Use this template

Click the "Use this template" button on GitHub or clone this repository:

```bash
git clone https://github.com/carvalhocaio/intentions
cd intentions
```

### 2. Install dependencies

```bash
bun install
```

### 3. Start development server

```bash
bun run dev
```

The server will start on `http://localhost:3333` with hot reload enabled.

## Available Scripts

| Script | Description |
|--------|-------------|
| `bun run dev` | Start development server with hot reload |
| `bun run start` | Start production server |
| `bun run format` | Format and lint code with Biome |

## API Documentation

Once the server is running, you can access the interactive API documentation at:

- **Scalar UI**: [http://localhost:3333/docs](http://localhost:3333/docs)

The documentation is automatically generated from your route schemas.

## Project Structure

```
.
├── src/
│   └── server.ts          # Main server file with example routes
├── biome.json             # Biome configuration
├── package.json           # Dependencies and scripts
├── tsconfig.json          # TypeScript configuration
└── README.md              # This file
```

## Usage Example

### Creating a New Route

```typescript
app.post(
  '/users',
  {
    schema: {
      tags: ['Users'],
      description: 'Create a new user',
      body: z.object({
        name: z.string(),
        email: z.string().email(),
      }),
      response: {
        201: z.object({
          id: z.string(),
          name: z.string(),
          email: z.string(),
        }),
      },
    },
  },
  async (request, reply) => {
    const { name, email } = request.body
    
    // Your business logic here
    
    return reply.status(201).send({
      id: '123',
      name,
      email,
    })
  }
)
```

### Type-Safe Validation

Zod schemas provide automatic:
- Request validation (body, query, params)
- Response validation
- TypeScript type inference
- OpenAPI documentation generation

## Configuration

### Port Configuration

Change the port in `src/server.ts`:

```typescript
await app.listen({ port: 3333, host: "0.0.0.0" })
```

### CORS Configuration

Modify CORS settings in `src/server.ts`:

```typescript
await app.register(fastifyCors, {
  origin: true, // or specify allowed origins
  methods: ["GET", "POST", "PUT", "PATCH", "DELETE", "OPTIONS"],
})
```

### API Documentation

Update API info in `src/server.ts`:

```typescript
await app.register(fastifySwagger, {
  openapi: {
    info: {
      title: "Your API Name",
      description: "Your API Description",
      version: "1.0.0",
    },
  },
  transform: jsonSchemaTransform,
})
```

## Dependencies

### Runtime
- **fastify**: Fast and low overhead web framework
- **@fastify/cors**: CORS support
- **@fastify/swagger**: OpenAPI documentation
- **@scalar/fastify-api-reference**: Beautiful API documentation UI
- **fastify-type-provider-zod**: Type-safe schemas with Zod
- **zod**: TypeScript-first schema validation

### Development
- **@biomejs/biome**: Fast formatter and linter
- **@types/bun**: TypeScript definitions for Bun

## Contributing

Feel free to contribute to this template by opening issues or pull requests.

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## Useful Links

- [Bun Documentation](https://bun.sh/docs)
- [Fastify Documentation](https://fastify.dev/)
- [Zod Documentation](https://zod.dev/)
- [Biome Documentation](https://biomejs.dev/)
