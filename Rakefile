def get_excludes
  exclude  = %w(.git .gitignore README.md RakeFile)

  if (File.exists?('.gitignore'))
    File.open('.gitignore', 'r').each_line do |line|
      exclude.push(line) unless exclude.include? line
    end
  end

  exclude
end

exclude = get_excludes

desc 'Install dotfiles'
task :install do

  current_dir = File.dirname(__FILE__)
  Dir.foreach(current_dir) do |item|
    next if item  == '.' or item == '..' or exclude.include? item or item[0] == '.'
    src  = current_dir + "/#{item}"
    dest = File.expand_path('~') + "/.#{item}"
    File.symlink(src, dest) && puts("Symlinking #{dest} -> #{src}") unless File.symlink?(dest) || File.exists?(dest)
  end

  puts "Installation complete!"

end

task :default => [:install]