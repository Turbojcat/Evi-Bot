# Command Creation Guide

This guide explains how to create commands for ThasiniaBot using the modular system.

## 🎯 Command Structure

Every command must follow this structure:

```typescript
import { SlashCommandBuilder, ChatInputCommandInteraction } from 'discord.js';
import { Command } from '../../types';
import { EmbedUtils } from '../../utils/embeds';

const yourCommand: Command = {
  data: new SlashCommandBuilder()
    .setName('commandname')
    .setDescription('Command description'),
  
  aliases: ['alias1', 'alias2'], // Optional
  description: 'Detailed description of what the command does',
  usage: '/commandname [options]',
  permissionLevel: 'user', // user, mod, admin, or dev

  async execute(interaction: ChatInputCommandInteraction) {
    // Your command logic here
    await interaction.reply({ 
      embeds: [EmbedUtils.success('Success!', 'Your command worked!')] 
    });
  }
};

export default yourCommand;
```

## 📁 File Organization

Commands are automatically loaded from the `src/commands/` directory. The folder structure determines the category:

```
src/commands/
├── general/          # General utility commands
│   ├── help.ts
│   └── ping.ts
├── utility/          # Utility commands
│   ├── help.ts
│   ├── ping.ts
│   ├── poll.ts
│   ├── announce.ts
│   ├── avatar.ts
│   ├── serverinfo.ts
│   ├── userinfo.ts
│   └── stats.ts
├── economy/          # Economy system commands
│   ├── economy.ts
│   ├── daily.ts
│   ├── weekly.ts
│   ├── monthly.ts
│   └── currency.ts
├── admin/           # Administrative commands
│   ├── welcome.ts
│   ├── logging.ts
│   ├── automod.ts
│   ├── statistics.ts
│   ├── trialmodrole.ts
│   ├── modrole.ts
│   ├── adminrole.ts
│   ├── serverdevrole.ts
│   ├── promote.ts
│   ├── demote.ts
│   ├── permissions.ts
│   ├── permissionlist.ts
│   └── currency.ts
├── dev/             # Developer commands
│   ├── reload.ts
│   └── premiumstatus.ts
├── botowner/        # Bot owner commands
│   ├── premium.ts
│   └── legalaccess.ts
├── setup/           # Setup commands
│   ├── welcome.ts
│   └── poll.ts
├── moderation/      # Moderation commands
│   ├── ban.ts
│   ├── unban.ts
│   └── clear.ts
├── fun/             # Fun and entertainment
│   ├── 8ball.ts
│   └── coinflip.ts
├── legal/           # Legal document commands
│   ├── premium.ts
│   ├── policy.ts
│   ├── tos.ts
│   └── license.ts
└── info/            # Information commands
    ├── serverinfo.ts
    ├── userinfo.ts
    └── stats.ts
```

## 🛡️ Permission Levels

The bot uses its own permission system:

- **`user`**: Basic commands available to everyone
- **`trialmod`**: Limited moderation capabilities
- **`mod`**: Moderation and management commands
- **`admin`**: Administrative and configuration commands
- **`sdev`**: Server developer privileges
- **`sowner`**: Server owner level
- **`dev`**: Bot development and maintenance commands
- **`botowner`**: Full bot control

Guild owners automatically have `sowner` permissions. Bot owner (BOTOWNER_ID) has `botowner` permissions.

## 🎨 Using Embeds

Always use the `EmbedUtils` for consistent styling:

```typescript
import { EmbedUtils } from '../../utils/embeds';

// Success message
await interaction.reply({
  embeds: [EmbedUtils.success('Title', 'Description')]
});

// Error message
await interaction.reply({
  embeds: [EmbedUtils.error('Error', 'Something went wrong')]
});

// Warning message
await interaction.reply({
  embeds: [EmbedUtils.warning('Warning', 'Be careful!')]
});

// Info message
await interaction.reply({
  embeds: [EmbedUtils.info('Info', 'Here is some information')]
});

// Custom embed
await interaction.reply({
  embeds: [EmbedUtils.createEmbed({
    title: 'Custom Title',
    description: 'Custom description',
    color: '#FF0000',
    fields: [
      { name: 'Field 1', value: 'Value 1', inline: true },
      { name: 'Field 2', value: 'Value 2', inline: true }
    ]
  })]
});
```

## 🔧 Command Options

You can add various options to your commands:

```typescript
data: new SlashCommandBuilder()
  .setName('example')
  .setDescription('Example command with options')
  .addStringOption(option =>
    option
      .setName('text')
      .setDescription('Enter some text')
      .setRequired(true)
  )
  .addUserOption(option =>
    option
      .setName('user')
      .setDescription('Select a user')
      .setRequired(false)
  )
  .addIntegerOption(option =>
    option
      .setName('number')
      .setDescription('Enter a number')
      .setRequired(false)
      .setMinValue(1)
      .setMaxValue(100)
  )
  .addChannelOption(option =>
    option
      .setName('channel')
      .setDescription('Select a channel')
      .setRequired(false)
  )
  .addRoleOption(option =>
    option
      .setName('role')
      .setDescription('Select a role')
      .setRequired(false)
  )
```

## 📝 Handling Options

Access options in your execute function:

```typescript
async execute(interaction: ChatInputCommandInteraction) {
  const text = interaction.options.getString('text', true); // Required
  const user = interaction.options.getUser('user'); // Optional
  const number = interaction.options.getInteger('number'); // Optional
  const channel = interaction.options.getChannel('channel'); // Optional
  const role = interaction.options.getRole('role'); // Optional

  // Your logic here
}
```

## 🔄 Automatic Loading

Commands are automatically loaded when:

1. The bot starts up
2. You use the `/reload` command (admin only)

No need to manually register commands or restart the bot!

## 📚 Example Commands

### Simple Command
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

### Command with Options
```typescript
// src/commands/economy/economy.ts
import { SlashCommandBuilder, ChatInputCommandInteraction, Message } from 'discord.js';
import { Command } from '../../types';
import { EmbedUtils } from '../../utils/embeds';
import { databaseManager } from '../../utils/database';

const economy: Command = {
  data: new SlashCommandBuilder()
    .setName('economy')
    .setDescription('Economy system commands')
    .addSubcommand(subcommand =>
      subcommand
        .setName('balance')
        .setDescription('Check your or another user\'s balance')
        .addUserOption(option =>
          option
            .setName('user')
            .setDescription('The user to check balance for')
            .setRequired(false)
        )
    )
    .addSubcommand(subcommand =>
      subcommand
        .setName('transfer')
        .setDescription('Transfer money to another user')
        .addUserOption(option =>
          option
            .setName('user')
            .setDescription('The user to transfer money to')
            .setRequired(true)
        )
        .addIntegerOption(option =>
          option
            .setName('amount')
            .setDescription('Amount of money to transfer')
            .setRequired(true)
            .setMinValue(1)
        )
    ),
  
  aliases: ['eco', 'economy', 'balance', 'bal', 'money', 'cash', 'transfer', 'pay', 'send', 'give'],
  description: 'Economy system - balance, transfer, leaderboard, and admin functions',
  usage: '/economy [@user] | /economy <transfer|leaderboard|add|remove|set|reset> [@user] [amount] [reason]',
  permissionLevel: 'user',

  async execute(interaction: ChatInputCommandInteraction | Message, args?: string[]) {
    // Command logic here
    // Supports both slash commands and prefix commands
    // Handles multiple subcommands: balance, transfer, leaderboard, admin commands
  }
};

export default economy;
```

## 🚀 Best Practices

1. **Always use embeds** for responses
2. **Check permissions** in your command logic if needed
3. **Handle errors gracefully** with try-catch blocks
4. **Use descriptive names** for commands and options
5. **Provide helpful descriptions** and usage examples
6. **Test your commands** before deploying
7. **Follow the existing code style** for consistency

## 🔧 Troubleshooting

### Command not loading?
- Check the file structure matches the expected format
- Ensure the command exports correctly
- Check for TypeScript compilation errors
- Use `/reload` to refresh commands

### Permission denied?
- Verify the permission level is correct
- Check if the user has the required permissions
- Guild owners always have `dev` permissions

### Options not working?
- Make sure option names match exactly
- Check if options are marked as required correctly
- Verify option types match your usage

## 📖 Additional Resources

- Check existing commands in `src/commands/` for examples
- Read the main README.md for setup instructions
- Look at the TypeScript types in `src/types/index.ts`
- Review the embed utilities in `src/utils/embeds.ts`
