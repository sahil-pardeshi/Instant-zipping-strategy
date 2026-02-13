# 7zip-instant-zipping-strategy
   Create Zip of Artifact After Build With Less Time

# For windows Install:
  on powershell install zip:
  `choco install 7zip -y`

Zip using 7-Zip: 
`"C:\Program Files\7-Zip\7z.exe" a -mx=1 D:\Build\aws.zip D:\Aws-Console-Learning-Platform\*`

# Description for each command: 
       <br>
       "C:\Program Files\7-Zip\7z.exe"  ---> This is the path where you installed 7-Zip  (Runs 7-Zip executable)
       <br>
       a  ---> add file to archive
       <br>
       -mx=1 ---> Fast compression (much faster than default)
       <br>
       D:\Build\aws.zip ---> after zip this is the location where your zip file get stored (Output ZIP file)
       <br>
       D:\Aws-Console-Learning-Platform\* ---> this is the actual file location which you zipped

# Deployment Archive using gzip

This guide explains how to install **gzip** on Linux and create a deployment archive from your project’s `Deploy` folder. This method is fast, reliable, and suitable for CI/CD pipelines.

---

##  Install gzip

Most Linux distributions come with gzip pre-installed. To check if gzip is installed, run:

```bash
gzip --version
```

# If gzip not installed 

On ubuntu

```bash
sudo apt update
sudo apt install gzip -y
```

On REHL/CentOs/Fedora

```
sudo yum install gzip -y
```

# 2️⃣ Prepare the Deploy Folder

Ensure you have a folder named Deploy containing only the files needed for deployment. Example structure:
```
Deploy/
├── server.js
├── package.json
├── package-lock.json
├── node_modules/
└── photos/
```

# Tip: For Node.js apps, install only production dependencies to reduce archive size:
```
npm ci --only=production
```

# For .NET apps, copy only the published output:
```
dotnet publish -c Release -o Deploy
```
# 3️⃣ Create a Deployment Archive

Use tar with gzip to compress the folder:

```
tar -czf app.tar.gz -C Deploy .
```
    Explanation:

    tar → Linux archiving tool

    -c → create a new archive

    -z → compress using gzip

    -f app.tar.gz → name of the output archive

    -C Deploy → change directory to Deploy before archiving

    . → include all files inside Deploy

This will generate a fast, compressed archive named app.tar.gz ready for deployment.

# 4️⃣ Optional: Fast Compression Mode
To prioritize speed over maximum compression:

```
tar -czf app.tar.gz -C Deploy . --fast
```
--fast or gzip -1 creates archives faster

Ideal for large directories like node_modules or photos

# 5️⃣ Verify the Archive

To check the contents of the archive:

```
tar -tzf app.tar.gz
```
This lists all files in the archive so you can confirm only required files are included.
