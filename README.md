Problem: Github Action to deploy Next.js project to Github pages is exiting with error code 1 during build job.

Solution: Create or update next.config.js to contain output: 'export'
i.e.
```
const nextConfig = {
  output: 'export'
}
 
module.exports = nextConfig
```

delete the next export command from the .yml file.
```
      - name: Build with Next.js
        run: ${{ steps.detect-package-manager.outputs.runner }} next build
      XX --> - name: Static HTML export with Next.js <-- XX
      XX --> run: ${{ steps.detect-package-manager.outputs.runner }} next export <-- XX
      - name: Upload artifact
        uses: actions/upload-pages-artifact@v3
```
