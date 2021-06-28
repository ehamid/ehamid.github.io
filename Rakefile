GH_PAGES_DIR = "compiled_site.io"

desc "Build Jekyll site and copy files"
task :build do
  system "rm -r -f _site/*"
  system "bundler exec jekyll build"
  system "rm -r ../#{GH_PAGES_DIR}/*" unless Dir['../#{GH_PAGES_DIR}/*'].empty?
  system "cp -r _site/* ../#{GH_PAGES_DIR}/"
  system "cd ../compiled_site.io; git add --all; git commit -m \"site update\"; git push"
end
