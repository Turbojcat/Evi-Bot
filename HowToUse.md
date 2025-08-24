# How To Use ThasiniaBot - Complete Guide

This document explains how everything works in the ThasiniaBot project so a new person can get everything working.

## 🚀 Quick Start Guide

### Prerequisites
- Node.js 18+ installed
- PostgreSQL database set up
- Discord Bot Token from Discord Developer Portal
- Git (for version control)

### Initial Setup

1. **Clone and Install**
   ```bash
   git clone <repository-url>
   cd ThasiniaBot
   npm install
   ```

2. **Configure Environment**
   ```bash
   npm run setup
   ```
   This will create your `.env` file with all necessary configuration.

3. **Set up Database**
   ```bash
   # Create PostgreSQL database
   createdb thasinia_bot
   
   # Run database migrations (when implemented)
   npm run migrate
   ```

4. **Build and Deploy**
   ```bash
   npm run build
   npm run deploy
   ```

5. **Start the Bot**
   ```bash
   npm start
   ```

## 📁 Project Structure Explained

```
ThasiniaBot/
├── src/
│   ├── commands/           # All bot commands organized by category
│   │   ├── general/       # General utility commands
│   │   ├── moderation/    # Moderation commands
│   │   ├── fun/          # Fun and entertainment
│   │   ├── admin/        # Administrative commands
│   │   ├── info/         # Information commands
│   │   └── economy/      # Economy system commands
│   ├── managers/          # Core system managers
│   │   ├── CommandManager.ts    # Handles command loading
│   │   ├── HelpManager.ts       # Handles help system
│   │   └── DatabaseManager.ts   # Handles database operations
│   ├── utils/            # Utility functions
│   │   ├── config.ts     # Configuration management
│   │   ├── embeds.ts     # Embed creation utilities
│   │   ├── permissions.ts # Permission system
│   │   └── database.ts   # Database utilities
│   ├── types/            # TypeScript type definitions
│   │   └── index.ts      # All type definitions
│   ├── database/         # Database related files
│   │   ├── migrations/   # Database migrations
│   │   ├── models/       # Database models
│   │   └── queries/      # Database queries
│   ├── Bot.ts           # Main bot class
│   ├── index.ts         # Entry point
│   └── deploy-commands.ts # Command deployment script
├── docs/                # Additional documentation
├── tests/               # Test files
├── package.json         # Dependencies and scripts
├── tsconfig.json        # TypeScript configuration
├── .env.example         # Environment variables template
├── setup.js            # Interactive setup script
├── README.md           # Main project documentation
├── COMMAND_GUIDE.md    # Command creation guide
└── HowToUse.md         # This file
```

## 🛠️ Core Systems Explained

### 1. Command System

The bot uses a **modular command system** that automatically loads commands from folders.

**How it works:**
- Commands are stored in `src/commands/[category]/[command].ts`
- Each command file exports a single command object
- The CommandManager automatically scans and loads all commands
- Commands are organized by category (general, moderation, fun, etc.)

**Command Structure:**
```typescript
import { SlashCommandBuilder, ChatInputCommandInteraction } from 'discord.js';
import { Command } from '../../types';
import { EmbedUtils } from '../../utils/embeds';

const exampleCommand: Command = {
  data: new SlashCommandBuilder()
    .setName('example')
    .setDescription('Example command'),
  
  aliases: ['ex', 'test'],
  description: 'What this command does',
  usage: '/example [options]',
  permissionLevel: 'user', // user, mod, admin, or dev

  async execute(interaction: ChatInputCommandInteraction) {
    // Command logic here
    await interaction.reply({
      embeds: [EmbedUtils.success('Success!', 'Command executed!')]
    });
  }
};

export default exampleCommand;
```

### 2. Permission System

The bot uses its **own permission system** instead of Discord permissions.

**Permission Levels:**
- **👤 User**: Basic commands (everyone can use)
- **🛡️ Moderator**: Moderation commands
- **⚡ Administrator**: Administrative commands
- **👨‍💻 Developer**: Bot development commands

**How permissions work:**
- Guild owners automatically get 'dev' permissions
- Permissions are stored in the database
- Commands check permissions before executing
- Permission levels are hierarchical (dev > admin > mod > user)

### 3. Help System

The bot has an **interactive help system** with buttons and categories.

**Features:**
- Shows only commands the user has permission to use
- Organized by categories
- Interactive buttons for navigation
- Detailed command information (usage, aliases, permissions)
- Automatic updates when new commands are added

**Usage:**
- `/help` - Shows main help menu
- `/help [category]` - Shows commands in specific category
- `/help [command]` - Shows detailed help for specific command

### 4. Embed System

All bot responses use **consistent embeds** for beautiful formatting.

**Available embed types:**
```typescript
import { EmbedUtils } from '../utils/embeds';

// Success message (green)
EmbedUtils.success('Title', 'Description');

// Error message (red)
EmbedUtils.error('Error', 'Something went wrong');

// Warning message (yellow)
EmbedUtils.warning('Warning', 'Be careful!');

// Info message (blue)
EmbedUtils.info('Info', 'Here is information');

// Custom embed
EmbedUtils.createEmbed({
  title: 'Custom Title',
  description: 'Custom description',
  color: '#FF0000',
  fields: [
    { name: 'Field 1', value: 'Value 1', inline: true }
  ]
});
```

### 5. Database System

The bot uses **PostgreSQL** for all data storage.

**What's stored in database:**
- User permissions
- Guild settings
- Economy data
- Moderation logs
- Custom configurations

**Database structure:**
```sql
-- Users table
CREATE TABLE users (
  user_id VARCHAR(20) PRIMARY KEY,
  permission_level VARCHAR(10) DEFAULT 'user',
  created_at TIMESTAMP DEFAULT NOW()
);

-- Guilds table
CREATE TABLE guilds (
  guild_id VARCHAR(20) PRIMARY KEY,
  prefix VARCHAR(5) DEFAULT '!',
  welcome_channel VARCHAR(20),
  log_channel VARCHAR(20),
  created_at TIMESTAMP DEFAULT NOW()
);

-- Economy table
CREATE TABLE economy (
  user_id VARCHAR(20) PRIMARY KEY,
  balance INTEGER DEFAULT 0,
  last_daily TIMESTAMP,
  created_at TIMESTAMP DEFAULT NOW()
);
```

## 🎯 How to Add New Commands

### Step 1: Create Command File
Create a new file in the appropriate category folder:
```bash
# Example: Create a fun command
touch src/commands/fun/hello.ts
```

### Step 2: Write Command Code
```typescript
// src/commands/fun/hello.ts
import { SlashCommandBuilder, ChatInputCommandInteraction } from 'discord.js';
import { Command } from '../../types';
import { EmbedUtils } from '../../utils/embeds';

const hello: Command = {
  data: new SlashCommandBuilder()
    .setName('hello')
    .setDescription('Say hello to the bot'),
  
  aliases: ['hi', 'hey'],
  description: 'The bot will greet you back',
  usage: '/hello',
  permissionLevel: 'user',

  async execute(interaction: ChatInputCommandInteraction) {
    const user = interaction.user;
    await interaction.reply({
      embeds: [EmbedUtils.success(
        'Hello!', 
        `Nice to meet you, ${user.username}! 👋`
      )]
    });
  }
};

export default hello;
```

### Step 3: Command is Automatically Loaded
- The bot will automatically detect and load your new command
- No need to restart the bot (unless you want to use `/reload`)
- The command will appear in the help system automatically

## 🔧 Development Workflow

### 1. Development Mode
```bash
npm run dev
```
This starts the bot with hot reload - changes are automatically detected.

### 2. Testing Commands
```bash
# Build the project
npm run build

# Deploy commands to Discord
npm run deploy

# Start the bot
npm start
```

### 3. Adding Database Features
When adding commands that need data storage:

1. **Create database migration:**
   ```bash
   # Create new migration file
   touch src/database/migrations/001_create_users_table.sql
   ```

2. **Write migration:**
   ```sql
   -- src/database/migrations/001_create_users_table.sql
   CREATE TABLE IF NOT EXISTS users (
     user_id VARCHAR(20) PRIMARY KEY,
     permission_level VARCHAR(10) DEFAULT 'user',
     created_at TIMESTAMP DEFAULT NOW()
   );
   ```

3. **Create database utility:**
   ```typescript
   // src/utils/database.ts
   export async function getUserPermission(userId: string): Promise<string> {
     const result = await db.query(
       'SELECT permission_level FROM users WHERE user_id = $1',
       [userId]
     );
     return result.rows[0]?.permission_level || 'user';
   }
   ```

4. **Use in command:**
   ```typescript
   import { getUserPermission } from '../../utils/database';
   
   // In your command
   const permission = await getUserPermission(interaction.user.id);
   ```

## 🚨 Troubleshooting

### Common Issues and Solutions

**1. Bot not starting:**
```bash
# Check if .env file exists and has correct values
cat .env

# Check if dependencies are installed
npm install

# Check for TypeScript errors
npm run build
```

**2. Commands not loading:**
```bash
# Check command file structure
ls src/commands/

# Use reload command in Discord
/reload

# Check console for error messages
```

**3. Database connection issues:**
```bash
# Check if PostgreSQL is running
sudo systemctl status postgresql

# Check database connection
psql -d thasinia_bot -c "SELECT 1;"

# Check environment variables
echo $DATABASE_URL
```

**4. Permission issues:**
- Guild owners automatically have 'dev' permissions
- Check if user has been assigned permissions in database
- Use admin commands to set user permissions

### Debug Mode
Enable debug logging by setting in `.env`:
```env
DEBUG=true
LOG_LEVEL=debug
```

## 📚 Available Commands

### General Commands
- `/help` - Show help menu
- `/ping` - Check bot latency
- `/info` - Show bot information

### Moderation Commands
- `/kick` - Kick a user
- `/ban` - Ban a user
- `/warn` - Warn a user
- `/mute` - Mute a user

### Fun Commands
- `/8ball` - Ask magic 8-ball
- `/joke` - Get a random joke
- `/roll` - Roll dice
- `/coinflip` - Flip a coin

### Admin Commands
- `/reload` - Reload all commands
- `/promote` - Promote user to higher permission level
- `/demote` - Demote user to lower permission level
- `/permissions` - Check user permission level
- `/permissionlist` - Show all permission levels
- `/legalaccess` - Access legal ownership info (BOTOWNER only)

### Info Commands
- `/serverinfo` - Show server information
- `/userinfo` - Show user information
- `/botinfo` - Show bot statistics

## 🔄 Maintenance

### Regular Tasks
1. **Update dependencies:**
   ```bash
   npm update
   npm audit fix
   ```

2. **Backup database:**
   ```bash
   pg_dump thasinia_bot > backup_$(date +%Y%m%d).sql
   ```

3. **Check logs:**
   ```bash
   tail -f logs/bot.log
   ```

4. **Monitor performance:**
   - Check memory usage
   - Monitor database performance
   - Review error logs

### Updates
When updating the bot:
1. Stop the bot
2. Pull latest changes: `git pull`
3. Install new dependencies: `npm install`
4. Run database migrations: `npm run migrate`
5. Build and deploy: `npm run build && npm run deploy`
6. Start the bot: `npm start`

## 🆘 Getting Help

If you need help:
1. Check this document first
2. Look at the README.md file
3. Check the COMMAND_GUIDE.md for command creation help
4. Review existing commands in `src/commands/` for examples
5. Check the console logs for error messages
6. Ask in the development Discord server

## 📝 Contributing

When contributing to the project:
1. Follow the established code style
2. Add proper TypeScript types
3. Use embeds for all responses
4. Test your commands thoroughly
5. Update documentation if needed
6. Follow the permission system
7. Use the database for data storage

---

**Remember:** This document should always be kept updated with any new features or changes to the bot system!
