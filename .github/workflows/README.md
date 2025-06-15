# SafeSpace AI Backend

The backend service for SafeSpace AI, providing emotional support through AI-powered conversations and group vent pods.

## Features

- User authentication and authorization
- AI-powered emotional support chat
- Real-time group vent pods
- Crisis detection and appropriate guidance
- Rate limiting and security measures
- MongoDB integration for data persistence
- WebSocket support for real-time communication

## Prerequisites

- Node.js (v14 or higher)
- MongoDB Atlas account
- OpenAI API key

## Setup

1. Clone the repository
2. Install dependencies:
   ```bash
   npm install
   ```

3. Create a `.env` file:
   ```bash
   cp .env.example .env
   ```

4. Update the `.env` file with your configuration:
   - MongoDB connection string
   - JWT secret key
   - OpenAI API key
   - Other configuration as needed

5. Start the development server:
   ```bash
   npm run dev
   ```

## API Endpoints

### Authentication
- `POST /api/auth/register` - Register a new user
- `POST /api/auth/login` - Login user
- `GET /api/auth/profile` - Get user profile
- `PATCH /api/auth/profile` - Update user profile

### Chat
- `POST /api/chat/start` - Start a new chat session
- `POST /api/chat/message` - Send a message
- `GET /api/chat/history` - Get chat history
- `POST /api/chat/:chatId/end` - End a chat session

### Vent Pods
- `POST /api/ventpods` - Create a new vent pod
- `GET /api/ventpods` - Get all vent pods
- `GET /api/ventpods/:ventPodId` - Get specific vent pod
- `POST /api/ventpods/:ventPodId/join` - Join a vent pod
- `POST /api/ventpods/:ventPodId/leave` - Leave a vent pod
- `PATCH /api/ventpods/:ventPodId` - Update vent pod
- `DELETE /api/ventpods/:ventPodId` - Delete vent pod

## WebSocket Events

### Vent Pod Events
- `join-ventpod` - Join a vent pod room
- `leave-ventpod` - Leave a vent pod room
- `vent-message` - Send a message to a vent pod
- `new-vent` - Receive a new message in a vent pod

## Security Features

- JWT-based authentication
- Password hashing with bcrypt
- Rate limiting
- CORS protection
- Helmet security headers
- Input validation
- Error handling

## Development

### Running Tests
```bash
npm test
```

### Code Style
The project uses ESLint for code linting. Run:
```bash
npm run lint
```

## Deployment

The backend is designed to be deployed on Render. Follow these steps:

1. Create a new Web Service on Render
2. Connect your GitHub repository
3. Set the following environment variables:
   - `MONGODB_URI`
   - `JWT_SECRET`
   - `OPENAI_API_KEY`
   - `NODE_ENV=production`
   - `FRONTEND_URL` (your frontend URL)

4. Set the build command:
   ```bash
   npm install
   ```

5. Set the start command:
   ```bash
   npm start
   ```

## Contributing

1. Fork the repository
2. Create your feature branch
3. Commit your changes
4. Push to the branch
5. Create a new Pull Request

## License

This project is licensed under the MIT License - see the LICENSE file for details. 