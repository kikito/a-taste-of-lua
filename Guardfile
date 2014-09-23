guard :shell, :all_on_start => true do
  watch("a-taste-of-lua.md") { regen }
  watch("css/style.css")       { regen }
end

def regen
  system('rm -rf a-taste-of-lua')
  system('mdpress -i images a-taste-of-lua.md')
  system('rm -rf a-taste-of-lua/css')
  system('cp -r css a-taste-of-lua')
end
