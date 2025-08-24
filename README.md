# 🤖 Evi Bot - Multipurpose Discord Bot

<div align="center">

[![Discord](https://img.shields.io/badge/Discord-Join%20Support%20Server-7289DA?style=for-the-badge&logo=discord&logoColor=white)](https://discord.gg/6tnqjeRach)
[![License](https://img.shields.io/badge/License-Evi%20License%20Agreement-purple.svg?style=for-the-badge)](license.md)
[![TypeScript](https://img.shields.io/badge/TypeScript-007ACC?style=for-the-badge&logo=typescript&logoColor=white)](https://www.typescriptlang.org/)
[![Node.js](https://img.shields.io/badge/Node.js-18+-green?style=for-the-badge&logo=node.js)](https://nodejs.org/)

**🌟 Welcome to Evi Bot - Your Ultimate Discord Companion! 🌟**

> **Evi is a multipurpose Discord bot, containing fun, games, moderation, utility and so much more.**

[![Add to Discord](https://img.shields.io/badge/Add%20to%20Discord-7289DA?style=for-the-badge&logo=discord&logoColor=white)](https://discord.com/oauth2/authorize?client_id=1242259937808220262&permissions=8&integration_type=0&scope=bot)

**Join our community and experience the power of Evi Bot!**

</div>

## 📋 Table of Contents

- [🌟 Features](#-features)
- [🚀 Quick Start](#-quick-start)
- [⚙️ Configuration](#️-configuration)
- [📚 Commands](#-commands)
- [🔐 Permission System](#-permission-system)
- [💎 Premium System](#-premium-system)
- [⚖️ Legal Framework](#️-legal-framework)
- [🏗️ Architecture](#️-architecture)
- [📁 File Structure](#-file-structure)
- [🔧 Development](#-development)
- [📖 Documentation](#-documentation)
- [🤝 Support](#-support)

## 🌟 Features

### 🎮 **Core Features**
- **Modular Command System** - Easy to add new commands by simply creating folders
- **Dual Command Support** - Both prefix (`!`) and slash (`/`) commands
- **Auto Tab Completion** - Intelligent command suggestions
- **Interactive Help System** - Beautiful embed-based help with category navigation
- **Hot Reload** - Reload commands without restarting the bot

### 🔐 **Advanced Permission System**
- **8 Permission Levels**: User, Trialmod, Mod, Admin, Sdev, Sowner, DEV, BOTOWNER
- **Database Integration** - Persistent permission storage
- **Role-based Access** - Granular control over command access
- **Cache System** - Fast permission lookups

### 💎 **Premium System**
- **Free Tier** - Basic bot functionality with community support
- **Premium (€10/month)** - Enhanced features and priority support
- **Lifetime (€200)** - One-time payment for permanent access
- **Source Code (€1000)** - Full intellectual property rights (with restrictions)

### 🗄️ **Database & Storage**
- **SQLite Integration** - Built-in database management
- **Automatic Setup** - No manual database configuration required
- **Data Persistence** - User data, settings, and statistics
- **Usage Tracking** - Command usage and user activity logs

### ⚖️ **Legal Framework**
- **Comprehensive Legal Documents** - Premium, Policy, ToS, License
- **Bulletproof Protection** - No legal loopholes
- **Source Code Protection** - Strict resale prohibition with €10,000 penalty
- **Data Protection** - GDPR compliant privacy policy

## 🚀 Quick Start

### Prerequisites
- Node.js 18+ 
- npm 8+
- Discord Bot Token

### Installation

1. **Clone the repository** (Contact on on support server)
   ```bash
   git clone https://github.com/Turbojcat/Evi-Bot.git
   cd Evi-Bot
   ```

2. **Install dependencies**
   ```bash
   npm install
   ```

3. **Configure environment**
   ```bash
   # Copy and edit .env file
   cp .env.example .env
   ```

4. **Build the project**
   ```bash
   npm run build
   ```

5. **Deploy commands**
   ```bash
   npm run deploy
   ```

6. **Start the bot**
   ```bash
   npm start
   ```

## ⚙️ Configuration

### Environment Variables (.env)

```env
# Bot Configuration
BOT_TOKEN=your_discord_bot_token
CLIENT_ID=your_client_id
CLIENT_SECRET=your_client_secret
BOT_INVITE_LINK=your_bot_invite_link

# Database
DATABASE_NAME=evi_bot.db

# Bot Info
BOT_NAME=Evi
BOT_VERSION=0.0.1
BOT_AUTHOR=Thasinia Sarcyne
BOT_LANGUAGE=TS

# Embed Colors
EMBED_COLOR_PRIMARY=#7a23e4
EMBED_COLOR_SUCCESS=#00ff00
EMBED_COLOR_ERROR=#ff0000
EMBED_COLOR_WARNING=#ffff00
EMBED_COLOR_INFO=#0099ff

# Permissions
BOT_OWNER_ID=315927854523219968
DEV_IDS=dev_id_1,dev_id_2

# Premium System
SUPPORT_SERVER_INVITE=6tnqjeRach
PREMIUM_PRICE_MONTHLY=10
PREMIUM_PRICE_LIFETIME=200
PREMIUM_PRICE_SOURCE_CODE=1000
LEGAL_ACCESS_PASSWORD=123
```

## 📚 Commands

### 🎯 **General Commands**
| Command | Description | Usage | Permission |
|---------|-------------|-------|------------|
| `/help` | Shows interactive help menu | `/help [category] [command]` | User |
| `/ping` | Check bot latency | `/ping` | User |
| `/serverinfo` | Display server information | `/serverinfo` | User |

### 🔧 **Admin Commands**
| Command | Description | Usage | Permission |
|---------|-------------|-------|------------|
| `/reload` | Reload all commands | `/reload` | Admin |
| `/legalaccess` | Access legal ownership info | `/legalaccess` | BOTOWNER |

### ⚖️ **Legal Commands**
| Command | Description | Usage | Permission |
|---------|-------------|-------|------------|
| `/premium` | View premium terms | `/premium` | User |
| `/policy` | View privacy policy | `/policy` | User |
| `/tos` | View terms of service | `/tos` | User |
| `/license` | View license agreement | `/license` | User |

### 📊 **Command Categories**
- **General** - Basic utility commands
- **Admin** - Administrative functions
- **Info** - Information and status
- **Legal** - Legal documents and terms
- **Premium** - Premium features (coming soon)
- **Fun** - Entertainment commands (coming soon)
- **Games** - Game-related commands (coming soon)
- **Moderation** - Server moderation (coming soon)
- **Economy** - Currency system (coming soon)
- **Music** - Music playback (coming soon)

## 🔐 Permission System

### Permission Levels (Hierarchy)

1. **User** - Basic access to general commands
2. **Trialmod** - Limited moderation capabilities
3. **Mod** - Full moderation access
4. **Admin** - Server administration
5. **Sdev** - Server developer privileges
6. **Sowner** - Server owner level
7. **DEV** - Bot developer access
8. **BOTOWNER** - Full bot control

### Permission Features
- **Database Storage** - Permissions persist across restarts
- **Cache System** - Fast permission lookups
- **Role Management** - Easy promotion/demotion
- **Override System** - BOTOWNER and DEV bypass all restrictions

## 💎 Premium System

### Free Tier
- ✅ Basic bot functionality
- ✅ Standard commands
- ✅ Community support
- ✅ Ticket support

### Premium (€10/month)
- ✅ All Free features
- ✅ Enhanced commands
- ✅ Priority support
- ✅ Advanced features

### Lifetime (€200)
- ✅ All Premium features
- ✅ Permanent access
- ✅ No monthly payments
- ✅ Lifetime updates

### Source Code (€1000)
- ✅ Full intellectual property rights
- ✅ Complete source code access
- ✅ Custom modifications allowed
- ⚠️ **Strict Usage Restrictions**
  - Only for buyer's own servers
  - Must have Discord Administrator permission
  - No resale allowed (€10,000 penalty)
  - No ownership transfer

## ⚖️ Legal Framework

### Legal Documents
- **[Premium Terms](legal/Premium.md)** - Premium service terms
- **[Privacy Policy](legal/Policy.md)** - Data protection and privacy
- **[Terms of Service](legal/ToS.md)** - Service usage terms
- **[License Agreement](legal/license.md)** - Software licensing

### Key Legal Features
- **Bulletproof Protection** - No legal loopholes
- **Source Code Protection** - Strict resale prohibition
- **Data Protection** - GDPR compliant
- **Clear Terms** - Easy to understand language

## 🏗️ Architecture

### Core Components

#### **CommandManager**
- Dynamic command loading from folders
- Category organization
- Command validation
- Statistics tracking

#### **PermissionManager**
- Database-integrated permissions
- Cache system for performance
- Role hierarchy management
- Override system for special users

#### **DatabaseManager**
- SQLite database management
- Automatic table creation
- CRUD operations
- Data persistence

#### **HelpManager**
- Interactive help system
- Category navigation
- Permission filtering
- Premium feature display

### Framework Features
- **Modular Design** - Easy to extend and maintain
- **Type Safety** - Full TypeScript support
- **Error Handling** - Comprehensive error management
- **Performance** - Optimized for speed and efficiency

## 📁 File Structure

```
ThasiniaBot/
├── src/
│   ├── commands/           # Command modules
│   │   ├── admin/         # Administrative commands
│   │   ├── general/       # General utility commands
│   │   ├── info/          # Information commands
│   │   └── legal/         # Legal document commands
│   ├── managers/          # Core framework managers
│   │   ├── CommandManager.ts
│   │   ├── HelpManager.ts
│   │   └── PermissionManager.ts
│   ├── utils/             # Utility functions
│   │   ├── config.ts      # Configuration management
│   │   ├── database.ts    # Database operations
│   │   ├── embeds.ts      # Embed utilities
│   │   └── permissions.ts # Permission utilities
│   ├── types/             # TypeScript type definitions
│   │   └── index.ts
│   ├── Bot.ts             # Main bot class
│   ├── index.ts           # Entry point
│   └── deploy-commands.ts # Command deployment
├── legal/                 # Legal documents
│   ├── Premium.md
│   ├── Policy.md
│   ├── ToS.md
│   └── license.md
├── .env                   # Environment configuration
├── package.json           # Project metadata
├── tsconfig.json          # TypeScript configuration
└── README.md              # This file
```

## 🔧 Development

### Available Scripts

```bash
npm run build      # Compile TypeScript
npm run start      # Start the bot
npm run dev        # Development mode with hot reload
npm run watch      # Watch mode for development
npm run clean      # Clean build directory
npm run deploy     # Deploy slash commands
npm run setup      # Initial setup
```

### Development Guidelines

#### **Adding New Commands**
1. Create a new file in the appropriate category folder
2. Follow the command structure template
3. Include proper permission levels
4. Add help documentation
5. Test thoroughly before deployment

#### **Command Structure**
```typescript
import { SlashCommandBuilder, ChatInputCommandInteraction, Message } from 'discord.js';

export default {
  data: new SlashCommandBuilder()
    .setName('commandname')
    .setDescription('Command description'),
  
  description: 'Detailed command description',
  usage: '!commandname [optional] <required>',
  aliases: ['alias1', 'alias2'],
  permissionLevel: 'user' as const,
  
  async execute(interaction: ChatInputCommandInteraction | Message, args?: string[]) {
    // Command implementation
  }
};
```

#### **Code Standards**
- Use TypeScript with strict typing
- Follow consistent naming conventions
- Include proper error handling
- Document all functions and classes
- Test all changes before deployment

## 📖 Documentation

### Additional Documentation
- **[HowToUse.md](HowToUse.md)** - Comprehensive usage guide
- **[Legal Documents](legal/)** - All legal terms and conditions
- **[Command Guide](CommandGuide.md)** - Detailed command reference

### API Reference
- **Discord.js v14** - [Official Documentation](https://discord.js.org/)
- **TypeScript** - [Official Documentation](https://www.typescriptlang.org/)
- **SQLite** - [Official Documentation](https://www.sqlite.org/)

## 🤝 Support

### Getting Help
- **Support Server**: [Join our Discord](https://discord.gg/6tnqjeRach)
- **Issues**: [GitHub Issues](https://github.com/Turbojcat/Evi-Bot/issues)
- **Documentation**: Check the docs folder for detailed guides

### Contributing
1. Fork the repository
2. Create a feature branch
3. Make your changes
4. Test thoroughly
5. Submit a pull request

### Premium Support
- **Premium Users**: Priority support via Discord tickets
- **Lifetime Users**: Dedicated support channel access
- **Source Code Buyers**: Direct developer support

---

## 📄 License

This project is licensed under the Evi License Agreement - see the [license.md](license.md) file for details.

## 🚀 Quick Actions

<div align="center">

[![Add to Discord](https://img.shields.io/badge/Add%20to%20Discord-7289DA?style=for-the-badge&logo=discord&logoColor=white)](https://discord.com/oauth2/authorize?client_id=1242259937808220262&permissions=8&integration_type=0&scope=bot)
[![Support Server](https://img.shields.io/badge/Join%20Support%20Server-7289DA?style=for-the-badge&logo=discord&logoColor=white)](https://discord.gg/6tnqjeRach)
[![Report Issue](https://img.shields.io/badge/Report%20Issue-red?style=for-the-badge&logo=github)](https://github.com/Turbojcat/Evi-Bot/issues)
[![Donate](https://img.shields.io/badge/Donate%20via%20PayPal-00457C?style=for-the-badge&logo=paypal)](https://paypal.me/ThasiniaSarcyne)

</div>

## 💎 Premium Features

<div align="center">

| Tier | Price | Features |
|------|-------|----------|
| **Free** | €0 | Basic functionality, Community support |
| **Premium** | €10/month | Enhanced features, Priority support |
| **Lifetime** | €200 | Permanent access, All features |
| **Source Code** | €1000 | Full rights, Custom modifications |

[**Learn More About Premium →**](#-premium-system)

</div>

## 📊 Bot Statistics

<div align="center">

![GitHub stars](https://img.shields.io/github/stars/Turbojcat/Evi-Bot?style=for-the-badge&logo=github)
![GitHub forks](https://img.shields.io/github/forks/Turbojcat/Evi-Bot?style=for-the-badge&logo=github)
![GitHub issues](https://img.shields.io/github/issues/Turbojcat/Evi-Bot?style=for-the-badge&logo=github)
![GitHub pull requests](https://img.shields.io/github/issues-pr/Turbojcat/Evi-Bot?style=for-the-badge&logo=github)

</div>

## 👨‍💻 Author

<div align="center">

**Thasinia Sarcyne**

[![Discord](https://img.shields.io/badge/Discord-Support%20Server-7289DA?style=for-the-badge&logo=discord)](https://discord.gg/6tnqjeRach)
[![PayPal](https://img.shields.io/badge/Donate%20via%20PayPal-00457C?style=for-the-badge&logo=paypal)](https://paypal.me/ThasiniaSarcyne)
[![GitHub](https://img.shields.io/badge/GitHub-Profile-181717?style=for-the-badge&logo=github)](https://github.com/Turbojcat)

</div>

---

<div align="center">

**🌟 Made with ❤️ by Thasinia Sarcyne 🌟**

**Join thousands of users who trust Evi Bot for their Discord servers!**

[![Discord](https://img.shields.io/badge/Discord-Join%20Support%20Server-7289DA?style=for-the-badge&logo=discord&logoColor=white)](https://discord.gg/6tnqjeRach)
[![Add to Discord](https://img.shields.io/badge/Add%20to%20Discord-7289DA?style=for-the-badge&logo=discord&logoColor=white)](https://discord.com/oauth2/authorize?client_id=1242259937808220262&permissions=8&integration_type=0&scope=bot)

**⭐ Star this repository if you find Evi Bot helpful! ⭐**

</div>
