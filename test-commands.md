# Test Guide for Welcome, Leave, and Boost Commands

## 🧪 Testing the Commands

### 1. Welcome Command Testing

**Setup Welcome System:**
```
/welcome setup #general Welcome to {server}, {user}! 🎉
```
or
```
!welcome setup #general Welcome to {server}, {user}! 🎉
```

**Test Welcome Message:**
```
/welcome test
```
or
```
!welcome test
```

**Disable Welcome System:**
```
/welcome disable
```
or
```
!welcome disable
```

### 2. Leave Command Testing

**Setup Leave System:**
```
/leave setup #general Goodbye {user}! 👋
```
or
```
!leave setup #general Goodbye {user}! 👋
```

**Test Leave Message:**
```
/leave test
```
or
```
!leave test
```

**Disable Leave System:**
```
/leave disable
```
or
```
!leave disable
```

### 3. Boost Command Testing

**Setup Boost System:**
```
/boost setup #general Thanks {user} for boosting {server}! ⚡
```
or
```
!boost setup #general Thanks {user} for boosting {server}! ⚡
```

**Test Boost Message:**
```
/boost test
```
or
```
!boost test
```

**Disable Boost System:**
```
/boost disable
```
or
```
!boost disable
```

## 🔧 Advanced Message Formatting

### Plain and Embed Messages
You can set both plain text and embed messages:

**Welcome:**
```
/welcome setup #general plain Welcome {user}! | embed Welcome to {server}, {user}! 🎉
```

**Leave:**
```
/leave setup #general plain Goodbye {user}! | embed Thanks for being part of {server}, {user}! 👋
```

**Boost:**
```
/boost setup #general plain Thanks {user}! | embed {user} just boosted {server}! ⚡
```

## 📝 Available Variables

- `{user}` - Mentions the user
- `{server}` - Server name
- `{count}` - Member count

## 🐛 Troubleshooting

### If commands don't work:

1. **Check Permissions:** Make sure you have admin permissions
2. **Check Bot Permissions:** Bot needs to send messages in the target channel
3. **Check Database:** Make sure the database is properly initialized
4. **Check Logs:** Look for error messages in the console

### Common Issues:

1. **"Channel not found"** - The channel ID is invalid or bot doesn't have access
2. **"System not setup"** - Run the setup command first
3. **"Permission denied"** - Check your permission level

## 🔍 Debug Information

The bot now includes debug logging:
- Welcome events are logged when members join
- Leave events are logged when members leave  
- Boost events are logged when members start boosting

Check the console for these messages to verify the systems are working.
