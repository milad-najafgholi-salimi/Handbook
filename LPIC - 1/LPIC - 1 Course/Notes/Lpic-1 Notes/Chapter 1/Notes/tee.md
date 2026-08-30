`tee` reads from standard input and writes to standard output AND to one or more files simultaneously.

### Common Use Cases
#### 1. Save output while still seeing it on screen
```
# Without tee - output goes only to screen
ls -la

# With tee - output goes to screen AND file
ls -la | tee directory_listing.txt
```

#### 2. Append to existing files (instead of overwriting)
```
echo "New data" | tee -a existing_file.txt
```

#### 3. Write to multiple files at once
```
echo "Important message" | tee file1.txt file2.txt file3.txt
```

#### 4. Combine with sudo for root-owned files
```
# This doesn't work (redirection runs as user)
echo "config change" > /etc/config_file

# This works (tee runs with sudo)
echo "config change" | sudo tee /etc/config_file
```

#### 5. Use with pipes for logging
```
# Log errors and normal output separately
./build_script.sh 2>&1 | tee build.log

# Or log to file while piping to another command
cat data.txt | tee backup.txt | grep "pattern" | sort
```

### Useful Options
|Option|Description|
|---|---|
|`-a`|Append to files instead of overwriting|
|`-i`|Ignore interrupt signals (INT)|
