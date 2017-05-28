require 'fileutils'

# Usage: rake build
# No arguments are allowed to avoid deleting wrong directories by mistake
desc "Build this Jekyll site to a predefined folder"
task :build do

  DIR = './docs'

  # Remove current _site folder and local production folder
  FileUtils.rm_rf('./_site', :verbose => true)
  FileUtils.rm_rf(Dir.glob("#{DIR}/*"), :verbose => true)

  # Build Jekyll
  system 'jekyll build --safe'

  # Copy the new _site to local production folder
  FileUtils.cp_r(Dir.glob('./_site/*'), "#{DIR}/", :verbose => true)

  # Create and copy necessary files to production
  File.open("#{DIR}/CNAME", 'w+') {|f| f.write('cn.yizeng.me') }
  FileUtils.touch("#{DIR}/.nojekyll", :verbose => true)
  FileUtils.cp('.gitignore', "#{DIR}/", :verbose => true)

  # Compress html in _site
  Dir.glob("#{DIR}/**/*.html") do |html_file|
    puts "Compressing: #{html_file}"
    system "java -jar ./_rake/tools/htmlcompressor-1.5.3.jar --recursive --compress-js -o #{html_file} #{html_file}"
  end
end
