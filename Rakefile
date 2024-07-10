require "rake/clean"

CLEAN.include("gobook", "gen/*")

PROTO_DIR = "proto"
PROTO_GEN_DIR = "gen"
PROTO_FILES = FileList["#{PROTO_DIR}/*.proto"]
PROTO_INC = PROTO_FILES.dup
PROTO_INC.each_index { |t| PROTO_INC[t] = "#{PROTO_GEN_DIR}/".concat(File.basename(PROTO_INC[t], ".proto").concat(".pg.go")) }

rule ".pg.go" do |t|
  sh "protoc --go_out=#{PROTO_GEN_DIR} #{PROTO_DIR}/#{File.basename(t.name, ".pg.go")}.proto"
end

task gobook: PROTO_INC do |t|
  sh "go build"
end

task default: [:gobook] do
  puts "default done"
end
