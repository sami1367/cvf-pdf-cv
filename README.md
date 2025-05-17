# PDF Component Generator

A Nuxt 3 application that allows you to generate PDFs from Vue components. Built with html2pdf.js for PDF generation and Bootstrap for styling.

## Setup

Make sure to install dependencies:

```bash
# npm
npm install

# pnpm
pnpm install

# yarn
yarn install

# bun
bun install
```

## Development Server

Start the development server on `http://localhost:3000`:

```bash
# npm
npm run dev

# pnpm
pnpm dev

# yarn
yarn dev

# bun
bun run dev
```

## Features

- Dynamic component rendering
- PDF generation from any component
- Bootstrap styling
- Easy to add new components

## Usage

1. Access components through the dynamic route:
   ```
   http://localhost:3000/generate-pdf/SimpleCard    # View and generate PDF of the card component
   http://localhost:3000/generate-pdf/SimpleTable   # View and generate PDF of the table component
   ```

2. Add new components:
   - Create your component in the `components` directory
   - Import it in `pages/generate-pdf/[pdfcomponentname].vue`
   - Add it to the components object
   ```javascript
   import NewComponent from '~/components/NewComponent.vue'
   
   const components = {
     SimpleCard,
     SimpleTable,
     NewComponent  // Add your new component here
   }
   ```

## Production

Build the application for production:

```bash
# npm
npm run build

# pnpm
pnpm build

# yarn
yarn build

# bun
bun run build
```

Locally preview production build:

```bash
# npm
npm run preview

# pnpm
pnpm preview

# yarn
yarn preview

# bun
bun run preview
```

Check out the [deployment documentation](https://nuxt.com/docs/getting-started/deployment) for more information.
