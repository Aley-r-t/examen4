# Etapa 1: Construcción
FROM node:20 AS builder

# Crear directorio de trabajo
WORKDIR /app

# Copiar dependencias
COPY package*.json ./
RUN npm install

# Copiar el resto del proyecto y construir
COPY . .
RUN npm run build

# Etapa 2: Producción
FROM node:20

WORKDIR /app

# Copiamos solo el resultado del build
COPY --from=builder /app/dist ./dist
COPY --from=builder /app/package*.json ./

# Instalamos solo las dependencias necesarias para correr (no devDependencies)
RUN npm install --omit=dev

# Exponemos el puerto (puede ser 3000 o 4321 según configuración)
EXPOSE 3000

# Comando para ejecutar el SSR server
CMD ["node", "dist/server/entry.mjs"]
