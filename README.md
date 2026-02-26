# Next.js AI Chatbot

![Project Logo](app/(chat)/opengraph-image.png)

A production-ready AI chatbot template built with Next.js 15, the AI SDK, and xAI's Grok models. This template provides a complete foundation for building sophisticated AI-powered chat applications with authentication, file handling, artifact management, and more.

## Features

- **Advanced Chat Interface**
  - Real-time streaming responses with AI SDK
  - Multiple AI model support (chat and reasoning models)
  - Message history with pagination
  - Message voting system (upvote/downvote)
  - Chat visibility controls (public/private)

- **User Authentication**
  - Guest user access with limited functionality
  - Regular user registration and login
  - Secure password hashing with bcrypt
  - Session management with NextAuth.js v5

- **Artifacts System**
  - Create and edit documents in real-time
  - Code editor with syntax highlighting (Python, JavaScript)
  - Spreadsheet creation and editing
  - Image generation and display
  - Split-screen interface for chat and artifacts

- **File Management**
  - Image upload support (JPEG, PNG)
  - Vercel Blob storage integration
  - File size validation (max 5MB)

- **AI Capabilities**
  - Weather information tool
  - Document suggestion system
  - Content generation and editing
  - Geolocation-aware responses
  - Advanced reasoning model with think tags

- **UI/UX**
  - Dark/light theme support
  - Responsive design for mobile and desktop
  - Modern interface with shadcn/ui components
  - Smooth animations with Framer Motion
  - Toast notifications

## Tech Stack

### Frontend
- **Framework**: Next.js 15.3.0 (App Router)
- **UI Library**: React 19.0.0-rc
- **Styling**: Tailwind CSS 3.4.1
- **Components**: shadcn/ui (Radix UI primitives)
- **Icons**: Lucide React
- **Fonts**: Geist Sans & Geist Mono
- **Animations**: Framer Motion
- **Markdown**: react-markdown with remark-gfm
- **Code Editor**: CodeMirror 6
- **Theme**: next-themes

### Backend
- **Runtime**: Next.js Server Components & Server Actions
- **API**: Next.js API Routes
- **Authentication**: NextAuth.js 5.0.0-beta.25
- **Password Hashing**: bcrypt-ts

### Database
- **Database**: PostgreSQL (Vercel Postgres)
- **ORM**: Drizzle ORM 0.34.0
- **Migrations**: Drizzle Kit
- **Client**: postgres.js

### AI/ML
- **AI SDK**: Vercel AI SDK 4.3.4
- **AI Provider**: xAI (Grok models)
- **Models**: 
  - grok-2-vision-1212 (chat)
  - grok-3-mini-beta (reasoning)
  - grok-2-1212 (title/artifacts)
  - grok-2-image (image generation)

### Authentication
- **Provider**: NextAuth.js v5
- **Strategy**: Credentials (email/password)
- **Session**: JWT-based
- **User Types**: Guest, Regular

### Cloud
- **Hosting**: Vercel
- **Database**: Vercel Postgres
- **File Storage**: Vercel Blob
- **Analytics**: Vercel Analytics
- **Functions**: @vercel/functions (geolocation)

### DevOps
- **Package Manager**: pnpm 9.12.3
- **Linting**: ESLint, Biome
- **Formatting**: Biome, Prettier
- **Testing**: Playwright
- **Type Checking**: TypeScript 5.6.3

### Libraries
- **Validation**: Zod 3.23.8
- **Date Handling**: date-fns 4.1.0
- **Diff/patch**: diff-match-patch
- **CSV Parsing**: papaparse
- **UUID**: nanoid
- **State Management**: SWR
- **Custom Hooks**: usehooks-ts

### APIs
- **Weather**: Open-Meteo API
- **AI**: xAI API
- **Storage**: Vercel Blob API

### Deployment
- **Platform**: Vercel
- **Build**: Next.js build system
- **Environment**: Vercel Environment Variables

## Architecture

The application follows a modern Next.js App Router architecture with clear separation of concerns:

### Application Structure
- **App Router**: Uses Next.js 15 App Router with file-based routing
- **Server Components**: Leverages React Server Components for performance
- **Server Actions**: Implements server-side mutations for data operations
- **API Routes**: RESTful endpoints for external integrations

### Data Flow
1. **User Authentication**: Middleware intercepts requests → NextAuth validates session → JWT tokens manage state
2. **Chat Flow**: User sends message → API route validates → AI SDK processes with tools → Response streamed to client
3. **Artifact Creation**: AI triggers tool → Document saved to database → Real-time UI update
4. **File Upload**: Client uploads to Vercel Blob → URL returned → Attachment linked to message

### Key Patterns
- **Route Groups**: `(auth)` and `(chat)` for logical separation
- **Database Layer**: Drizzle ORM with type-safe queries
- **AI Integration**: Custom provider wrapper with model selection
- **State Management**: Server actions + client hooks (SWR)
- **Error Handling**: Try-catch blocks with user-friendly error messages

### Security
- **Middleware**: Route protection and authentication checks
- **Row-Level Security**: User ownership validation on all operations
- **Input Validation**: Zod schemas for API endpoints
- **Secrets Management**: Environment variables for sensitive data

## Folder Structure

```
nextjs-ai-chatbot/
├── app/                          # Next.js App Router
│   ├── (auth)/                   # Authentication route group
│   │   ├── actions.ts           # Auth server actions
│   │   ├── auth.config.ts       # NextAuth configuration
│   │   ├── auth.ts              # NextAuth setup
│   │   ├── api/auth/            # Auth API routes
│   │   ├── login/               # Login page
│   │   └── register/            # Registration page
│   ├── (chat)/                   # Chat route group
│   │   ├── actions.ts           # Chat server actions
│   │   ├── api/                 # Chat API routes
│   │   │   ├── chat/           # Chat endpoint
│   │   │   ├── document/       # Document CRUD
│   │   │   ├── files/          # File upload
│   │   │   ├── history/        # Chat history
│   │   │   ├── suggestions/    # Document suggestions
│   │   │   └── vote/           # Message voting
│   │   ├── chat/[id]/          # Individual chat page
│   │   ├── layout.tsx          # Chat layout
│   │   └── page.tsx            # Chat home
│   ├── favicon.ico             # Site favicon
│   ├── globals.css             # Global styles
│   └── layout.tsx              # Root layout
├── artifacts/                   # Artifact server components
│   ├── actions.ts              # Artifact server actions
│   ├── code/                   # Code artifacts
│   ├── image/                  # Image artifacts
│   ├── sheet/                  # Spreadsheet artifacts
│   └── text/                   # Text artifacts
├── components/                   # React components
│   ├── ui/                     # shadcn/ui components
│   ├── app-sidebar.tsx         # Application sidebar
│   ├── artifact.tsx            # Artifact component
│   ├── auth-form.tsx           # Authentication form
│   ├── chat.tsx                # Chat interface
│   ├── message.tsx             # Message component
│   └── ...                     # Other UI components
├── hooks/                       # Custom React hooks
│   ├── use-artifact.ts         # Artifact state management
│   ├── use-chat-visibility.ts  # Chat visibility state
│   ├── use-messages.tsx        # Message state management
│   └── ...                     # Other hooks
├── lib/                         # Library utilities
│   ├── ai/                     # AI integration
│   │   ├── models.ts           # AI model configuration
│   │   ├── providers.ts        # AI provider setup
│   │   ├── prompts.ts          # System prompts
│   │   ├── tools/              # AI tools
│   │   └── entitlements.ts     # User entitlements
│   ├── db/                     # Database layer
│   │   ├── schema.ts           # Database schema
│   │   ├── queries.ts          # Database queries
│   │   ├── migrations/         # Drizzle migrations
│   │   └── utils.ts            # DB utilities
│   ├── editor/                 # Rich text editor
│   ├── constants.ts            # Application constants
│   └── utils.ts                # General utilities
├── public/                      # Static assets
│   └── images/                 # Images
├── tests/                       # Playwright tests
│   ├── e2e/                    # End-to-end tests
│   ├── routes/                 # API route tests
│   └── ...                     # Test utilities
├── .env.example                 # Environment variables template
├── .eslintrc.json              # ESLint configuration
├── biome.jsonc                 # Biome configuration
├── components.json             # shadcn/ui configuration
├── drizzle.config.ts           # Drizzle configuration
├── middleware.ts                # Next.js middleware
├── next.config.ts              # Next.js configuration
├── package.json                # Dependencies and scripts
├── playwright.config.ts        # Playwright configuration
├── tailwind.config.ts          # Tailwind CSS configuration
├── tsconfig.json               # TypeScript configuration
└── LICENSE                     # Apache 2.0 license
```

## Prerequisites

Before running this project, ensure you have the following installed:

- **Node.js**: 18.x or higher (recommended: 20.x)
- **pnpm**: 9.12.3 or higher
- **PostgreSQL**: Access to a PostgreSQL database (Vercel Postgres recommended)
- **xAI API Key**: Get from [https://console.x.ai/](https://console.x.ai/)
- **Vercel Account**: For deployment and Vercel services (optional for local development)

### Required Services
- Vercel Postgres (or any PostgreSQL database)
- Vercel Blob (for file storage)
- xAI API access

## Installation

### Clone Repository

```bash
# Using Git
git clone https://github.com/your-username/nextjs-ai-chatbot.git
cd nextjs-ai-chatbot

# Or download and extract the ZIP file
```

### Install Dependencies

**Windows (PowerShell):**
```powershell
pnpm install
```

**macOS/Linux:**
```bash
pnpm install
```

### Configure Environment Variables

1. Copy the example environment file:
```bash
# Windows
copy .env.example .env.local

# macOS/Linux
cp .env.example .env.local
```

2. Edit `.env.local` and add your values:

```bash
# Generate a random secret: https://generate-secret.vercel.app/32
AUTH_SECRET=your-random-secret-here

# xAI API Key from https://console.x.ai/
XAI_API_KEY=your-xai-api-key-here

# Vercel Blob token from https://vercel.com/docs/storage/vercel-blob
BLOB_READ_WRITE_TOKEN=your-blob-token-here

# PostgreSQL connection string
POSTGRES_URL=postgresql://user:password@host:port/database
```

### Database Setup

**Option 1: Vercel Postgres (Recommended)**
1. Create a Postgres database on Vercel
2. Copy the connection string to `POSTGRES_URL`
3. Run migrations:
```bash
pnpm db:push
```

**Option 2: Local PostgreSQL**
1. Install PostgreSQL locally
2. Create a database:
```bash
createdb ai_chatbot
```
3. Set your connection string in `.env.local`:
```bash
POSTGRES_URL=postgresql://localhost:5432/ai_chatbot
```
4. Run migrations:
```bash
pnpm db:push
```

### Migrations

The project uses Drizzle ORM for database management:

```bash
# Generate migration from schema changes
pnpm db:generate

# Apply migrations to database
pnpm db:migrate

# Push schema changes directly (development)
pnpm db:push

# Open Drizzle Studio (database GUI)
pnpm db:studio
```

### Seed Data

Not found in the current codebase. The application creates guest users dynamically as needed.

## Environment Variables

| Variable | Required | Description | Example |
|----------|----------|-------------|---------|
| `AUTH_SECRET` | Yes | Secret key for NextAuth.js session encryption | `random-32-character-string` |
| `XAI_API_KEY` | Yes | API key for xAI (Grok models) | `xai-api-key-here` |
| `BLOB_READ_WRITE_TOKEN` | Yes | Token for Vercel Blob storage access | `blob-read-write-token` |
| `POSTGRES_URL` | Yes | PostgreSQL connection string | `postgresql://user:pass@host:5432/db` |
| `NODE_ENV` | No | Environment mode (development/production) | `development` |

### Variable Details

**AUTH_SECRET**
- Required for NextAuth.js to encrypt session tokens
- Generate at https://generate-secret.vercel.app/32
- Or use: `openssl rand -base64 32`

**XAI_API_KEY**
- Required for AI model access
- Get your key at https://console.x.ai/
- Supports both chat and image models

**BLOB_READ_WRITE_TOKEN**
- Required for file upload functionality
- Create a Blob store on Vercel
- Instructions: https://vercel.com/docs/storage/vercel-blob

**POSTGRES_URL**
- Required for database connectivity
- Format: `postgresql://[user]:[password]@[host]:[port]/[database]`
- Can use Vercel Postgres or any PostgreSQL instance

## Running the Project

### Development Mode

**Windows (PowerShell):**
```powershell
pnpm dev
```

**macOS/Linux:**
```bash
pnpm dev
```

The application will start at [http://localhost:3000](http://localhost:3000)

### Production Mode

**Build the application:**
```bash
pnpm build
```

**Start production server:**
```bash
pnpm start
```

### Docker

Not found in the current codebase. Docker support is not implemented.

## API Documentation

### Chat Endpoints

#### POST /api/chat
Create a new chat message and get AI response.

- **Authentication**: Required
- **Request Body**:
```json
{
  "id": "chat-uuid",
  "message": {
    "id": "message-uuid",
    "role": "user",
    "parts": [{"type": "text", "text": "Hello"}]
  },
  "selectedChatModel": "chat-model"
}
```
- **Response**: Streaming text response with AI message

#### DELETE /api/chat
Delete a chat by ID.

- **Authentication**: Required
- **Query Parameters**: `id` (chat UUID)
- **Response**: Deleted chat object

### Document Endpoints

#### GET /api/document
Get document by ID.

- **Authentication**: Required
- **Query Parameters**: `id` (document UUID)
- **Response**: Document object with content

#### POST /api/document
Create or update a document.

- **Authentication**: Required
- **Query Parameters**: `id` (document UUID)
- **Request Body**:
```json
{
  "content": "Document content",
  "title": "Document Title",
  "kind": "text"
}
```
- **Response**: Saved document object

#### DELETE /api/document
Delete document after timestamp.

- **Authentication**: Required
- **Query Parameters**: `id`, `timestamp`
- **Response**: Deleted documents

### File Upload Endpoints

#### POST /api/files/upload
Upload a file to Vercel Blob.

- **Authentication**: Required
- **Content-Type**: `multipart/form-data`
- **Form Data**: `file` (Blob, max 5MB, JPEG/PNG only)
- **Response**: Uploaded file URL and metadata

### History Endpoints

#### GET /api/history
Get user's chat history with pagination.

- **Authentication**: Required
- **Query Parameters**:
  - `limit` (default: 10)
  - `starting_after` (cursor for next page)
  - `ending_before` (cursor for previous page)
- **Response**: Paginated chat list with `hasMore` flag

### Suggestions Endpoints

#### GET /api/suggestions
Get suggestions for a document.

- **Authentication**: Required
- **Query Parameters**: `documentId`
- **Response**: Array of suggestions

### Vote Endpoints

#### GET /api/vote
Get votes for a chat.

- **Authentication**: Required
- **Query Parameters**: `chatId`
- **Response**: Array of votes

#### PATCH /api/vote
Vote on a message.

- **Authentication**: Required
- **Request Body**:
```json
{
  "chatId": "chat-uuid",
  "messageId": "message-uuid",
  "type": "up"
}
```
- **Response**: Success message

### Auth Endpoints

#### GET /api/auth/guest
Create or sign in as guest user.

- **Authentication**: Not required
- **Query Parameters**: `redirectUrl` (optional)
- **Response**: Redirects to authenticated session

## Database

### Schema Overview

The application uses PostgreSQL with the following main tables:

#### User
```typescript
{
  id: uuid (primary key)
  email: varchar(64)
  password: varchar(64) (hashed)
}
```

#### Chat
```typescript
{
  id: uuid (primary key)
  createdAt: timestamp
  title: text
  userId: uuid (foreign key → User.id)
  visibility: enum('public', 'private')
}
```

#### Message_v2
```typescript
{
  id: uuid (primary key)
  chatId: uuid (foreign key → Chat.id)
  role: varchar
  parts: json (message content)
  attachments: json (file attachments)
  createdAt: timestamp
}
```

#### Vote_v2
```typescript
{
  chatId: uuid (foreign key → Chat.id)
  messageId: uuid (foreign key → Message_v2.id)
  isUpvoted: boolean
  (primary key: chatId + messageId)
}
```

#### Document
```typescript
{
  id: uuid
  createdAt: timestamp
  title: text
  content: text
  kind: enum('text', 'code', 'image', 'sheet')
  userId: uuid (foreign key → User.id)
  (primary key: id + createdAt)
}
```

#### Suggestion
```typescript
{
  id: uuid (primary key)
  documentId: uuid
  documentCreatedAt: timestamp
  originalText: text
  suggestedText: text
  description: text
  isResolved: boolean
  userId: uuid (foreign key → User.id)
  createdAt: timestamp
}
```

### Relationships

- **User → Chat**: One-to-many (a user can have multiple chats)
- **Chat → Message**: One-to-many (a chat can have multiple messages)
- **Chat → Vote**: One-to-many (a chat can have multiple votes)
- **Message → Vote**: One-to-one (a message can have one vote per user)
- **User → Document**: One-to-many (a user can have multiple documents)
- **Document → Suggestion**: One-to-many (a document can have multiple suggestions)

### Deprecated Tables

The following tables are deprecated and will be removed:
- `Message` (replaced by `Message_v2`)
- `Vote` (replaced by `Vote_v2`)

## Authentication

### User Types

The application supports two user types:

1. **Guest Users**
   - Created automatically when accessing without authentication
   - Email format: `guest-{timestamp}`
   - Limited to 20 messages per day
   - Temporary sessions

2. **Regular Users**
   - Created through registration
   - Requires email and password
   - Limited to 100 messages per day
   - Persistent sessions

### Authentication Flow

1. **Registration**
   - User provides email and password
   - Password is hashed with bcrypt
   - User record created in database
   - User automatically signed in

2. **Login**
   - User provides credentials
   - Password verified against hash
   - JWT session token created
   - Redirect to chat interface

3. **Guest Access**
   - Middleware detects unauthenticated request
   - Guest user created automatically
   - Session established with guest type
   - Redirect to original destination

### Session Management

- **Storage**: JWT tokens in HTTP-only cookies
- **Duration**: Session-based (configurable)
- **Security**: Secure cookies in production
- **Middleware**: Validates session on protected routes

### Password Security

- **Hashing**: bcrypt with salt
- **Validation**: Minimum 6 characters
- **Storage**: Hashed passwords only (never plain text)

## Configuration

### Next.js Configuration (next.config.ts)

- **Partial Prerendering (PPR)**: Enabled for performance
- **Image Optimization**: Configured for avatar.vercel.sh
- **Experimental Features**: PPR enabled

### TypeScript Configuration (tsconfig.json)

- **Target**: ESNext
- **Module Resolution**: Bundler
- **Strict Mode**: Enabled
- **Path Aliases**: `@/*` maps to project root

### Tailwind Configuration (tailwind.config.ts)

- **Dark Mode**: Class-based
- **Theme**: Custom color scheme with CSS variables
- **Plugins**: Animation and typography
- **Font Family**: Geist Sans and Geist Mono

### Drizzle Configuration (drizzle.config.ts)

- **Schema**: `./lib/db/schema.ts`
- **Migrations**: `./lib/db/migrations`
- **Dialect**: PostgreSQL
- **Environment**: `.env.local`

### Biome Configuration (biome.jsonc)

- **Formatter**: Enabled with 2-space indentation
- **Linter**: Recommended rules with custom overrides
- **Line Width**: 80 characters
- **Quote Style**: Single quotes

### ESLint Configuration (.eslintrc.json)

- **Extends**: Next.js, TypeScript, Prettier, Tailwind
- **Plugins**: Tailwind CSS
- **Rules**: Custom class name handling
- **Ignore**: UI components directory

## Build Instructions

### Development Build

```bash
# Install dependencies
pnpm install

# Run development server
pnpm dev
```

### Production Build

```bash
# Install dependencies
pnpm install

# Run database migrations
pnpm db:migrate

# Build application
pnpm build

# Start production server
pnpm start
```

### Build Output

- **Directory**: `.next/`
- **Static Assets**: Optimized and hashed
- **Server Bundle**: Node.js server files
- **Client Bundle**: Optimized JavaScript

## Deployment

### Vercel Deployment (Recommended)

1. **Push to GitHub**
```bash
git add .
git commit -m "Initial commit"
git push origin main
```

2. **Deploy on Vercel**
- Import repository on Vercel
- Configure environment variables
- Add integrations:
  - xAI (Grok)
  - Vercel Postgres
  - Vercel Blob
- Deploy

3. **Environment Variables on Vercel**
- `AUTH_SECRET`: Use Vercel's secret generator
- `XAI_API_KEY`: Add from xAI console
- `BLOB_READ_WRITE_TOKEN`: Auto-created with Blob integration
- `POSTGRES_URL`: Auto-created with Postgres integration

### Manual Deployment

```bash
# Build application
pnpm build

# Export static files (if applicable)
pnpm export

# Deploy to your platform
# (platform-specific commands)
```

### Environment-Specific Builds

```bash
# Development build
NODE_ENV=development pnpm build

# Production build
NODE_ENV=production pnpm build
```

## Testing

### Playwright End-to-End Tests

**Run all tests:**
```bash
pnpm test
```

**Run specific test file:**
```bash
npx playwright test tests/e2e/chat.test.ts
```

**Run tests in headed mode:**
```bash
npx playwright test --headed
```

**View test report:**
```bash
npx playwright show-report
```

### Test Structure

- **E2E Tests**: `tests/e2e/` - Full user flows
- **Route Tests**: `tests/routes/` - API endpoint testing
- **Fixtures**: `tests/fixtures.ts` - Test data and utilities
- **Helpers**: `tests/helpers.ts` - Test helper functions

### Test Coverage

- Chat functionality
- Artifact creation and editing
- Authentication flows
- API routes
- Reasoning model
- Session management

## Scripts

### Available Scripts

| Script | Description |
|--------|-------------|
| `pnpm dev` | Start development server with Turbo |
| `pnpm build` | Build production bundle and run migrations |
| `pnpm start` | Start production server |
| `pnpm lint` | Run ESLint and Biome linter |
| `pnpm lint:fix` | Fix linting issues automatically |
| `pnpm format` | Format code with Biome |
| `pnpm db:generate` | Generate Drizzle migration from schema |
| `pnpm db:migrate` | Apply database migrations |
| `pnpm db:studio` | Open Drizzle Studio database GUI |
| `pnpm db:push` | Push schema changes directly to database |
| `pnpm db:pull` | Pull schema from database |
| `pnpm db:check` | Check migration files |
| `pnpm db:up` | Apply pending migrations |
| `pnpm test` | Run Playwright tests |

### Script Usage Examples

```bash
# Development with hot reload
pnpm dev

# Production deployment
pnpm build && pnpm start

# Database management
pnpm db:studio  # Open database GUI
pnpm db:push    # Sync schema to database

# Code quality
pnpm lint       # Check for issues
pnpm format     # Format code

# Testing
pnpm test       # Run all tests
```

## Usage Examples

### Starting a Chat

1. Navigate to [http://localhost:3000](http://localhost:3000)
2. Enter your message in the input field
3. Press Enter or click Send
4. AI responds with streaming text

### Creating Artifacts

**Ask the AI to create content:**
```
"Create a Python function to calculate fibonacci numbers"
```

The AI will:
1. Create a code artifact
2. Display it in the right panel
3. Show the code with syntax highlighting

### Uploading Images

1. Click the attachment icon in the chat input
2. Select an image (JPEG/PNG, max 5MB)
3. Image uploads to Vercel Blob
4. Image appears in chat with preview

### Managing Chat History

1. Click the sidebar toggle
2. View previous conversations
3. Click on a chat to resume
4. Delete chats with the delete button

### Switching AI Models

1. Click the model selector in the header
2. Choose between:
   - Chat model (general purpose)
   - Reasoning model (advanced thinking)

### Voting on Messages

1. Hover over a message
2. Click the thumbs up or thumbs down icon
3. Vote is saved to database

## Screenshots

> **Note**: Screenshots are not available in the current repository. 

**Expected Screenshots:**
- Main chat interface with sidebar
- Artifact editor with code highlighting
- Authentication forms (login/register)
- Mobile responsive views
- Dark theme interface

## Error Handling

### Common Issues and Solutions

#### Database Connection Errors

**Error**: `Failed to connect to database`

**Solutions**:
1. Verify `POSTGRES_URL` is correct in `.env.local`
2. Ensure PostgreSQL server is running
3. Check network connectivity
4. Verify database credentials

#### Authentication Errors

**Error**: `Unauthorized` or `Forbidden`

**Solutions**:
1. Check `AUTH_SECRET` is set
2. Clear browser cookies
3. Verify session token validity
4. Check middleware configuration

#### AI API Errors

**Error**: `Failed to get AI response`

**Solutions**:
1. Verify `XAI_API_KEY` is valid
2. Check xAI service status
3. Verify API quota/limits
4. Check network connectivity

#### File Upload Errors

**Error**: `Upload failed` or `File size exceeded`

**Solutions**:
1. Verify `BLOB_READ_WRITE_TOKEN` is set
2. Ensure file is under 5MB
3. Check file type (JPEG/PNG only)
4. Verify Vercel Blob configuration

#### Build Errors

**Error**: TypeScript or build errors

**Solutions**:
1. Run `pnpm lint` to check for issues
2. Ensure all dependencies are installed
3. Check TypeScript configuration
4. Clear `.next` cache: `rm -rf .next`

## Performance Notes

### Optimization Features

- **Partial Prerendering (PPR)**: Enabled for faster initial loads
- **Streaming Responses**: Real-time AI response streaming
- **Code Splitting**: Automatic route-based splitting
- **Image Optimization**: Next.js Image component usage
- **Font Optimization**: Subsetting and display swap
- **Database Indexing**: Foreign keys and primary indexes

### Performance Considerations

- **Database Queries**: Use indexed columns for filtering
- **Message Limits**: Pagination for large chat histories
- **File Sizes**: 5MB limit for uploads
- **AI Rate Limits**: User type-based message limits
- **Bundle Size**: Tree-shaking and code splitting

### Monitoring

- **Vercel Analytics**: Built-in performance monitoring
- **Error Tracking**: Console error logging
- **Database Performance**: Drizzle query logging

## Security Notes

### Security Measures

- **Password Hashing**: bcrypt with salt
- **Session Security**: HTTP-only, secure cookies
- **SQL Injection Prevention**: Parameterized queries (Drizzle ORM)
- **XSS Prevention**: React's built-in escaping
- **CSRF Protection**: NextAuth.js built-in protection
- **Row-Level Security**: User ownership validation
- **Input Validation**: Zod schema validation
- **Secret Management**: Environment variables

### Best Practices

1. **Never commit `.env` files** - Use `.env.example` as template
2. **Use strong `AUTH_SECRET`** - Generate cryptographically random secrets
3. **Rotate API keys regularly** - Update `XAI_API_KEY` periodically
4. **Limit file uploads** - Current 5MB limit enforced
5. **Monitor user activity** - Message limits per user type
6. **Keep dependencies updated** - Regular security updates
7. **Use HTTPS in production** - Always enable SSL/TLS

### Known Security Considerations

- Guest users have temporary accounts with limited access
- File uploads restricted to images only
- No third-party authentication providers configured
- Environment variables must be secured on deployment platform

## Limitations

### Current Limitations

1. **AI Models**: Only xAI (Grok) models configured
2. **File Types**: Only JPEG and PNG images supported
3. **Authentication**: Only email/password (no OAuth providers)
4. **Database**: PostgreSQL only (no multi-database support)
5. **Code Languages**: Primary support for Python and JavaScript
6. **User Types**: Only guest and regular (no paid tiers)
7. **Deployment**: Optimized for Vercel platform
8. **Testing**: Only Playwright E2E tests (no unit tests)

### Scalability Considerations

- Message limits: 20/day (guest), 100/day (regular)
- File size: 5MB maximum
- Database: Single PostgreSQL instance
- No horizontal scaling configuration

## Future Improvements

### Planned Features

- **OAuth Providers**: Google, GitHub, etc.
- **Multi-Model Support**: OpenAI, Anthropic, Cohere
- **Advanced File Support**: PDF, documents, videos
- **Collaboration Features**: Shared chats and documents
- **Analytics Dashboard**: Usage statistics and insights
- **Mobile App**: React Native or PWA
- **Voice Input/Output**: Speech recognition and TTS
- **Custom Prompts**: User-configurable system prompts
- **Export Options**: PDF, Markdown, JSON exports
- **API Rate Limiting**: Advanced rate limiting strategies

### Technical Improvements

- **Unit Tests**: Jest or Vitest for unit testing
- **E2E Coverage**: Expand Playwright test coverage
- **Performance Monitoring**: Integration with APM tools
- **Error Tracking**: Sentry integration
- **Caching Strategy**: Redis or similar caching layer
- **CDN Integration**: Static asset CDN
- **Database Optimization**: Query optimization and indexing
- **Docker Support**: Containerized deployment

## Contributing Guide

### Development Workflow

1. **Fork the repository**
2. **Create a feature branch**: `git checkout -b feature/amazing-feature`
3. **Make changes** following code style guidelines
4. **Test thoroughly**: `pnpm test`
5. **Lint and format**: `pnpm lint && pnpm format`
6. **Commit changes**: Use conventional commit messages
7. **Push to branch**: `git push origin feature/amazing-feature`
8. **Open a Pull Request**

### Code Style Guidelines

- **TypeScript**: Strict mode enabled
- **Formatting**: Biome with 2-space indentation
- **Components**: Functional components with hooks
- **Naming**: camelCase for variables, PascalCase for components
- **Comments**: Minimal, only for complex logic
- **Imports**: Grouped and organized

### Pull Request Requirements

- **Tests**: New features require test coverage
- **Documentation**: Update README and code comments
- **Breaking Changes**: Clearly document in PR description
- **Approval**: At least one maintainer approval required

### Issue Reporting

When reporting issues, include:
- Environment details (OS, Node version)
- Steps to reproduce
- Expected vs actual behavior
- Error messages and logs
- Screenshots if applicable

## Code Style

### TypeScript Configuration

- **Strict Mode**: Enabled
- **No Implicit Any**: Enabled
- **Null Checks**: Enabled
- **Type Checking**: Comprehensive type coverage

### Formatting Rules

- **Indentation**: 2 spaces
- **Line Width**: 80 characters
- **Quotes**: Single quotes for strings
- **Semicolons**: Always used
- **Trailing Commas**: Multi-line arrays/objects

### Linting Rules

- **ESLint**: Next.js, TypeScript, Tailwind CSS
- **Biome**: Additional linting and formatting
- **Custom Rules**: Tailwind class name handling

### Naming Conventions

- **Components**: PascalCase (e.g., `ChatInterface`)
- **Functions**: camelCase (e.g., `getUserById`)
- **Constants**: UPPER_SNAKE_CASE (e.g., `MAX_MESSAGES`)
- **Files**: kebab-case (e.g., `chat-interface.tsx`)

## License

This project is licensed under the Apache License 2.0.

**Copyright 2026 vallabhatech**
**Copyright 2024 Vercel, Inc.**

Licensed under the Apache License, Version 2.0 (the "License");
you may not use this file except in compliance with the License.
You may obtain a copy of the License at

    http://www.apache.org/licenses/LICENSE-2.0

Unless required by applicable law or agreed to in writing, software
distributed under the License is distributed on an "AS IS" BASIS,
WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
See the License for the specific language governing permissions and
limitations under the License.

## Authors

- **Vercel, Inc.** - Original template creation
- **vallabhatech** - Modifications and enhancements

## Acknowledgements

- **Vercel** - Next.js framework and AI SDK
- **xAI** - Grok AI models
- **Radix UI** - Accessible component primitives
- **shadcn** - UI component library
- **Drizzle** - Database ORM
- **NextAuth.js** - Authentication solution
- **Playwright** - E2E testing framework

## Version History

### Version 3.0.15
- Current stable release
- Enhanced artifact system
- Improved authentication flow
- Performance optimizations

### Previous Versions
- See git commit history for detailed changes

## FAQ

### Q: Can I use different AI models?

A: Yes, the AI SDK supports multiple providers. You can modify `lib/ai/providers.ts` to add OpenAI, Anthropic, or other providers.

### Q: How do I increase message limits?

A: Modify `lib/ai/entitlements.ts` to adjust `maxMessagesPerDay` for each user type.

### Q: Can I deploy to platforms other than Vercel?

A: Yes, but you'll need to adapt the Vercel-specific integrations (Postgres, Blob, Functions) to alternatives.

### Q: How do I add OAuth providers?

A: Add provider configuration in `app/(auth)/auth.ts` following NextAuth.js documentation.

### Q: Is the database schema customizable?

A: Yes, modify `lib/db/schema.ts` and run `pnpm db:generate` to create migrations.

### Q: Can I use this commercially?

A: Yes, under the Apache 2.0 license. See LICENSE file for details.

### Q: How do I report security issues?

A: Please contact the maintainers directly for security vulnerabilities. Do not open public issues.

### Q: What browsers are supported?

A: Modern browsers supporting ES2020+ (Chrome, Firefox, Safari, Edge latest versions).

## Contact

For questions, issues, or contributions:

- **GitHub Issues**: [Repository Issues](https://github.com/your-username/nextjs-ai-chatbot/issues)
- **Documentation**: [Chat SDK Docs](https://chat-sdk.dev)
- **Support**: [Vercel Support](https://vercel.com/support)

---

**Built with ❤️ using Next.js and AI SDK**
