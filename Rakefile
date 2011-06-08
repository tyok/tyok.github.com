require 'rake/clean'

LAYOUT_SRC = FileList.new('_includes/*.haml','_layouts/*.haml', 'index.haml')
LAYOUT_HTML = LAYOUT_SRC.ext('html')
SCSS = FileList.new('stylesheets/*.scss')
CSS = SCSS.ext('css')
LAYOUT = LAYOUT_HTML + CSS

CLOBBER.include('_site')
CLEAN.include('tags/*.*')
CLEAN.include(LAYOUT)

rule '.html' => ['.haml'] do |t|
    sh %{ haml -E utf-8 #{t.source} #{t.name.sub(/_haml\./,'.')} }
end

rule '.css' => ['.scss'] do |t|
    sh %{ sass -t compressed #{t.source} #{t.name} }
end

desc 'Generate html and css from sources'
task :build => LAYOUT do
end

desc 'Build and start server'
task :server => :default do
  sh %{ jekyll --server --safe }
end

desc "Generate html"
task :default => :build
