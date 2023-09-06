# Update Procedure

1. update posts etc.
2. run "bundle exec jekyll serve" to serve and interactively update
3. run "bundle exec jekyll build" to build the website into _site
4. delete everything but CNAME in the compiled_site folder
5. copy _site contents into compiled_site
6. run git add --all
7. run git commit -m "message"
8. run git push