# FireCollect

FireCollect is a powerful research tool that helps academics and researchers manage their papers, PDFs, and Zotero libraries. It features AI-powered search capabilities, PDF analysis, and seamless Zotero integration.

![FireCollect Interface](./public/firecollect-interface.png)

## Features

- 🔍 **Academic Paper Search**: Search and analyze academic papers with AI assistance
- 📄 **PDF Analysis**: Upload and analyze PDFs with automatic metadata extraction
- 📚 **Zotero Integration**: Connect and manage your Zotero library
- 🤖 **AI-Powered**: Intelligent paper analysis and chat capabilities
- 📱 **Modern UI**: Clean, responsive interface with dark mode support
- 🔐 **Secure**: Built-in authentication and API key management

## Prerequisites

Before you begin, ensure you have the following installed:
- Node.js (v18 or higher)
- npm or yarn
- Git
- Supabase account (for database and authentication)
- Firecrawl API key (for AI features)
- Vercel account (for deployment)

## Setup Instructions

### 1. Clone the repository
```bash
git clone https://github.com/sahariarpku/firecollect-10.git
cd firecollect-10
```

### 2. Install dependencies
```bash
npm install
# or
yarn install
```

### 3. Supabase Setup

#### a. Create a Supabase Project

1. Go to [Supabase Dashboard](https://supabase.com/dashboard)
2. Click "New Project"
3. Fill in your project details:
   - Name your project
   - Set a secure database password
   - Choose a region closest to your users
4. Wait for the project to be created

#### b. Get Your Project Credentials

1. Go to your project's dashboard
2. Navigate to Project Settings > API
3. Copy these values:
   - Project URL (under "Project URL")
   - Project API Keys (both `anon` and `service_role` keys)
   - Project Reference ID (under "Project Reference ID")
4. Go to Project Settings > Database
5. Copy your database password (or reset it if needed)

#### c. Configure Environment Variables

1. Copy the example environment file:
   ```bash
   cp .env.example .env.local
   ```

2. Update `.env.local` with your Supabase credentials:
   ```
   NEXT_PUBLIC_SUPABASE_URL=your_project_url
   NEXT_PUBLIC_SUPABASE_ANON_KEY=your_anon_key
   SUPABASE_SERVICE_ROLE_KEY=your_service_role_key
   SUPABASE_DB_PASSWORD=your_database_password
   SUPABASE_PROJECT_ID=your_project_id
   ```

#### d. Initialize Supabase

1. Install Supabase CLI:
   ```bash
   npm install supabase --save-dev
   ```

2. Initialize Supabase (this will create necessary configuration files):
   ```bash
   npx supabase init
   ```

3. Link your project:
   ```bash
   npx supabase link --project-ref your_project_id
   ```

4. Push the database schema:
   ```bash
   npx supabase db push
   ```

### 4. Vercel Deployment

#### a. Prepare for Deployment

1. Create a Vercel account at [vercel.com](https://vercel.com) if you haven't already
2. Install Vercel CLI:
   ```bash
   npm install -g vercel
   ```

3. Login to Vercel:
   ```bash
   vercel login
   ```

#### b. Deploy to Vercel

1. Push your code to GitHub if you haven't already:
   ```bash
   git add .
   git commit -m "Prepare for Vercel deployment"
   git push origin main
   ```

2. Go to [Vercel Dashboard](https://vercel.com/dashboard)
3. Click "New Project"
4. Import your GitHub repository
5. Configure the project:
   - Framework Preset: Next.js
   - Root Directory: ./
   - Build Command: npm run build
   - Output Directory: .next
   - Install Command: npm install

6. Add Environment Variables:
   - Go to Project Settings > Environment Variables
   - Add the following variables:
     ```
     NEXT_PUBLIC_SUPABASE_URL=your_project_url
     NEXT_PUBLIC_SUPABASE_ANON_KEY=your_anon_key
     SUPABASE_SERVICE_ROLE_KEY=your_service_role_key
     SUPABASE_DB_PASSWORD=your_database_password
     SUPABASE_PROJECT_ID=your_project_id
     ```

7. Deploy the project:
   ```bash
   vercel
   ```

#### c. Post-Deployment Setup

1. After deployment, go to your project's settings in Vercel
2. Add your custom domain if desired
3. Configure any additional settings like:
   - Environment Variables
   - Build & Development Settings
   - Git Integration
   - Team Collaboration

### 5. Local Development
```bash
npm run dev
# or
yarn dev
```

The application will be available at `http://localhost:3000`

## Project Structure

```
firecollect-10/
├── src/
│   ├── components/        # React components
│   ├── services/         # API and service integrations
│   ├── lib/             # Utility functions and configurations
│   ├── types/           # TypeScript type definitions
│   └── app/             # Next.js app router files
├── public/              # Static assets
├── supabase/           # Supabase configurations and migrations
└── styles/             # Global styles and CSS modules
```

## Key Components

- **ResearchManager**: Handles academic paper search and analysis
- **PDFUploadView**: Manages PDF uploads and analysis
- **ZoteroConnect**: Handles Zotero library integration
- **UserProfile**: User settings and API key management

## Authentication

The app uses Supabase Authentication. Users can:
- Sign up with email/password
- Sign in with existing account
- Reset password
- Manage API keys and settings

## API Keys

Two types of API keys are required:
1. **Firecrawl API Key**: For AI-powered paper analysis
   - Get it from [firecrawl.dev](https://firecrawl.dev)
   - Add it in the user settings

2. **Zotero API Key**: For Zotero integration
   - Generate from [Zotero settings](https://www.zotero.org/settings/keys)
   - Add it when connecting Zotero

## Troubleshooting

### Common Database Issues

1. **Wrong Database Connection**
   - Ensure your environment variables are correctly set in Vercel
   - Make sure `supabase/config.toml` has the correct project ID
   - Try relinking your project:
     ```bash
     npx supabase link --project-ref your-project-id --debug
     ```

2. **Migration Errors**
   - Clear local Supabase configuration:
     ```bash
     rm -rf .supabase
     npx supabase init
     ```
   - Relink and push:
     ```bash
     npx supabase link --project-ref your-project-id
     npx supabase db push
     ```

3. **Permission Issues**
   - Verify your service role key has the correct permissions
   - Check RLS policies in Supabase dashboard

### Vercel Deployment Issues

1. **Build Failures**
   - Check build logs in Vercel dashboard
   - Verify all dependencies are in package.json
   - Ensure environment variables are properly set

2. **Runtime Errors**
   - Check Vercel deployment logs
   - Verify API endpoints are working
   - Test locally before deploying

3. **Environment Variables**
   - Double-check all required variables are set in Vercel
   - Ensure variables are properly formatted
   - Test with local environment variables

## Development

### Running Tests
```bash
npm run test
# or
yarn test
```

### Building for Production
```bash
npm run build
# or
yarn build
```

### Linting
```bash
npm run lint
# or
yarn lint
```

## Contributing

1. Fork the repository
2. Create your feature branch (`git checkout -b feature/AmazingFeature`)
3. Commit your changes (`git commit -m 'Add some AmazingFeature'`)
4. Push to the branch (`git push origin feature/AmazingFeature`)
5. Open a Pull Request

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## Support

For support, please open an issue in the GitHub repository or contact the maintainers.
