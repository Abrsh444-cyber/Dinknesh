src/app/api/chat/route.ts
+++ 23
--- 21
import { NextRequest, NextResponse } from "next/server";	import { NextRequest, NextResponse } from "next/server";
 	 
const SYSTEM_PROMPT = `You are an expert AI coding assistant similar to cto.new. You help developers with:	const SYSTEM_PROMPT = `You are an Ethiopian AI coding assistant named "የኢትዮጵያ AI ረዳት" (Ethiopian AI Helper). You help developers with:
- Writing clean, efficient, and well-documented code	- Writing clean, efficient, and well-documented code
- Debugging and fixing bugs	- Debugging and fixing bugs
- Code reviews and best practice suggestions	- Code reviews and best practice suggestions
- Task planning and project management	- Task planning and project management
When providing code examples, always use proper markdown code blocks with language identifiers.	When providing code examples, always use proper markdown code blocks with language identifiers.
Be concise but thorough. Ask clarifying questions when needed.`;	Be concise but thorough. Ask clarifying questions when needed.
You can respond in Amharic or English depending on the user's language.`;
 	 
function generateResponse(userMessage: string): string {	function generateResponse(userMessage: string): string {
  const lowerMsg = userMessage.toLowerCase();	  const lowerMsg = userMessage.toLowerCase();
 	 
  if (lowerMsg.includes("hello") || lowerMsg.includes("hi") || lowerMsg.includes("hey")) {	
    return `Hello! I'm your AI coding assistant. I can help you with:	  if (lowerMsg.includes("hello") || lowerMsg.includes("hi") || lowerMsg.includes("hey") || lowerMsg.includes("ሰላም") || lowerMsg.includes("አዎ") || lowerMsg.includes("ከሰላም")) {
    return `ሰላም! የኢትዮጵያ AI ረዳት ነኝ። እርስዎን ለማስተዋወቅ ደስ ብዬኛል። 
- **Code writing & review** – Write clean, efficient code in any language	
- **Debugging** – Identify and fix bugs in your code	
- **Architecture advice** – Design patterns, system design, and best practices	
- **Task planning** – Break down projects into manageable tasks	
- **Code analysis** – Performance, security, and quality insights	እኔ መርዳት እችላለሁ:
- **ኮድ መጻፍ** – በማንኛውም ቋንቋ ንፁህና ውጤታማ ኮድ መጻፍ
- **ስህተት ፈላጊ** – ኮድ ውስጥ ያሉትን ስህተቶች መለየትና ማስተካከል
- **አርክቲክቸር አማካሪ** – ዲዛይን ፓተርንስ፣ ስርዓት ዲዛይንና ምርጥ አሰራሮች
- **ተግባር እቅድ** – ፕሮጀክቶችን ወደ ሊታወቁ ተግባራት መከፋፈል
- **ኮድ ትንተካክል** – በፍጥነት፣ ደህንነትና ጥራት ላይ ግብዓቶች
What would you like to work on today?`;	 አሁን ምን LIRDAWOT?`;
  }	  }
 	 
  if (lowerMsg.includes("react") && (lowerMsg.includes("hook") || lowerMsg.includes("usestate"))) {	  if (lowerMsg.includes("react") && (lowerMsg.includes("hook") || lowerMsg.includes("usestate"))) {
Which area would you like to optimize specifically?`;	Which area would you like to optimize specifically?`;
  }	  }
  return `I understand you're asking about: **"${userMessage}"**	  return `እላዋለሁ ስለ: **"${userMessage}"**
 	 
I can help you with this. Here are some approaches to consider:	ለዚህ መርዳት እችላለሁ። እነዚህ አካሄዶች ይ� considered ናቸው:
 	 
1. **Analyze the requirements** – Break down what you need into clear, actionable steps	
2. **Choose the right tools** – Select appropriate libraries and frameworks for the task	
3. **Implement iteratively** – Start with a working solution, then optimize	
4. **Test thoroughly** – Write tests to verify your implementation works correctly	1. **መስፈርቱን መከላከል** – የሚያስፈልጉትን በቀላል እርምጃዎች መከፋፈል
2. **�正确的 መሣሪያዎችን መምረጥ** – ለሥራው ተስማሚዎችን ቤተ-ነበርዎችና ፍሪምወርክቶችን መምረጥ
3. **በማስመርቅ መተግበር** – በመጀመሪያ የሚሰራ መፍትሄ ይጀምሩ፣ ከዚያ ማመቻቸው
4. **በሙሉ መሞከር** – የሚሰራው በትክክል እንደሚሰራ ለማረጋገጥ ሙከራ ይጻፉ
 	 
To give you the most specific guidance, could you tell me:	
- What programming language or framework are you using?	
- What's the specific challenge you're facing?	
- Do you have any existing code I should consider?	ይልቅ የተለየ መመሪያ ለመስጠት፣ እባክዎ መናገር ይችላሉ:
- ምን የፕሮግራሚንግ ቋንቋ ወይም ፍሪምወርክ ነው የሚጠቀሙት?
- ምን የሆነ ልዩ ተግዳሜት ነው ያጋጠምዎት?
- እኔ መ� considered ነው የሚሆን ኮድ አለዎት?
 	 
You can also use the **Code Analysis** tab to paste your code and get instant feedback, or the **Tasks** tab to plan your work.`;	እንዲሁም **ኮድ ትንተካክል** ትርጉም ላይ ኮድ ማስገባት እና ፈጣን አስተያየት ማግኘት ይችላሉ፣ ወይም **ተግባር** ትርጉም ላይ ሥራዎችን ለማቀድ።`;
}	}
 	 
export async function POST(req: NextRequest) {	export async function POST(req: NextRequest) {

src/components/chat/ChatInterface.tsx
+++ 17
--- 17
import { Button } from "@/components/ui/Button";	import { Button } from "@/components/ui/Button";
 	 
const STARTER_PROMPTS = [	const STARTER_PROMPTS = [
  { icon: Code, label: "Review my code", prompt: "Can you review this code and suggest improvements?" },	
  { icon: Lightbulb, label: "Debug an issue", prompt: "Help me debug an error in my application" },	
  { icon: Sparkles, label: "Best practices", prompt: "What are the best practices for React performance?" },	
  { icon: Bot, label: "Plan a project", prompt: "Help me plan tasks for building a REST API" },	  { icon: Code, label: "ኮድ አስተያየት", prompt: "Can you review this code and suggest improvements?" },
  { icon: Lightbulb, label: "ስህተት ፈላጊ", prompt: "Help me debug an error in my application" },
  { icon: Sparkles, label: "የተሻሉ አሰራሮች", prompt: "What are the best practices for React performance?" },
  { icon: Bot, label: "ፕሮጀክት እቅድ", prompt: "Help me plan tasks for building a REST API" },
];	];
 	 
export function ChatInterface() {	export function ChatInterface() {
    } catch {	    } catch {
      addMessage(conversationId, {	      addMessage(conversationId, {
        role: "assistant",	        role: "assistant",
        content: "Sorry, I encountered an error. Please try again.",	        content: "ይቅርታ፣ ስህተት አጋጠምኝ። እባክዎ እንደገና ይሞክሩ።",
      });	      });
    } finally {	    } finally {
      setLoading(false);	      setLoading(false);
    <div className="flex h-full flex-col">	    <div className="flex h-full flex-col">
      <div className="border-b border-zinc-800 px-6 py-4">	      <div className="border-b border-zinc-800 px-6 py-4">
        <h2 className="text-base font-semibold text-white">	        <h2 className="text-base font-semibold text-white">
          {activeConversation?.title ?? "New Conversation"}	          {activeConversation?.title ?? "አዲስ ውይይት"}
        </h2>	        </h2>
        <p className="text-xs text-zinc-500 mt-0.5">	        <p className="text-xs text-zinc-500 mt-0.5">
          Ask anything about code, debugging, architecture, or best practices	          ለኮድ፣ ስህተት ፈላጊ፣ አርክቲክቸር ወይም ምርጥ አሰራሮች ማንኛውንም ጥያቄ ይጠይቁ
        </p>	        </p>
      </div>	      </div>
 	 
      <div className="flex-1 overflow-y-auto px-6 py-6 space-y-6">	      <div className="flex-1 overflow-y-auto px-6 py-6 space-y-6">
        {messages.length === 0 ? (	        {messages.length === 0 ? (
          <div className="flex h-full flex-col items-center justify-center">	          <div className="flex h-full flex-col items-center justify-center">
            <div className="flex h-14 w-14 items-center justify-center rounded-2xl bg-violet-600/20 border border-violet-600/30">	
              <Bot className="h-7 w-7 text-violet-400" />	            <div className="flex h-14 w-14 items-center justify-center rounded-2xl bg-green-600/20 border border-green-600/30">
              <Bot className="h-7 w-7 text-green-400" />
            </div>	            </div>
            <h3 className="mt-4 text-lg font-semibold text-white">	            <h3 className="mt-4 text-lg font-semibold text-white">
              How can I help you today?	              ዛም፣ እኔ እንዴት እርዳዎት?
            </h3>	            </h3>
            <p className="mt-2 text-sm text-zinc-500 text-center max-w-sm">	            <p className="mt-2 text-sm text-zinc-500 text-center max-w-sm">
              I&apos;m your AI coding assistant. Ask me anything about programming, debugging, or project planning.	              የኢትዮጵያ AI ረዳት ነኝ። ለፕሮግራሚንግ፣ ስህተት ፈላጊ ወይም ፕሮጀክት እቅድ ማንኛውንም ጥያቄ ይጠይቁ።
            </p>	            </p>
            <div className="mt-8 grid grid-cols-2 gap-3 w-full max-w-lg">	            <div className="mt-8 grid grid-cols-2 gap-3 w-full max-w-lg">
              {STARTER_PROMPTS.map(({ icon: Icon, label, prompt }) => (	              {STARTER_PROMPTS.map(({ icon: Icon, label, prompt }) => (
                <button	                <button
                  key={label}	                  key={label}
                  onClick={() => sendMessage(prompt)}	                  onClick={() => sendMessage(prompt)}
                  className="flex items-center gap-3 rounded-xl border border-zinc-700 bg-zinc-800/50 px-4 py-3 text-left text-sm text-zinc-300 transition-colors hover:border-violet-600/50 hover:bg-zinc-800 hover:text-white"	                  className="flex items-center gap-3 rounded-xl border border-zinc-700 bg-zinc-800/50 px-4 py-3 text-left text-sm text-zinc-300 transition-colors hover:border-green-600/50 hover:bg-zinc-800 hover:text-white"
                >	                >
                  <Icon className="h-4 w-4 text-violet-400 shrink-0" />	                  <Icon className="h-4 w-4 text-green-400 shrink-0" />
                  {label}	                  {label}
                </button>	                </button>
              ))}	              ))}
            ))}	            ))}
            {isLoading && (	            {isLoading && (
              <div className="flex gap-3">	              <div className="flex gap-3">
                <div className="flex h-8 w-8 shrink-0 items-center justify-center rounded-full bg-violet-600">	                <div className="flex h-8 w-8 shrink-0 items-center justify-center rounded-full bg-green-600">
                  <Bot className="h-4 w-4 text-white" />	                  <Bot className="h-4 w-4 text-white" />
                </div>	                </div>
                <div className="rounded-2xl rounded-tl-sm bg-zinc-800 px-4 py-3">	                <div className="rounded-2xl rounded-tl-sm bg-zinc-800 px-4 py-3">
              value={input}	              value={input}
              onChange={(e) => setInput(e.target.value)}	              onChange={(e) => setInput(e.target.value)}
              onKeyDown={handleKeyDown}	              onKeyDown={handleKeyDown}
              placeholder="Ask a coding question... (Enter to send, Shift+Enter for newline)"	              placeholder="ጥያቄ ይጠይቁ... (Enter ለማስርጣት, Shift+Enter ለአዲስ መስመር)"
              rows={1}	              rows={1}
              className="w-full resize-none rounded-xl border border-zinc-700 bg-zinc-800 px-4 py-2.5 text-sm text-zinc-100 placeholder-zinc-500 focus:border-violet-500 focus:outline-none focus:ring-1 focus:ring-violet-500 transition-colors"	              className="w-full resize-none rounded-xl border border-zinc-700 bg-zinc-800 px-4 py-2.5 text-sm text-zinc-100 placeholder-zinc-500 focus:border-green-500 focus:outline-none focus:ring-1 focus:ring-green-500 transition-colors"
              disabled={isLoading}	              disabled={isLoading}
            />	            />
          </div>	          </div>
          </Button>	          </Button>
        </div>	        </div>
        <p className="mt-2 text-xs text-zinc-600 text-center">	        <p className="mt-2 text-xs text-zinc-600 text-center">
          Press Enter to send · Shift+Enter for new line	          Enter ለማስርጣት · Shift+Enter ለአዲስ መስመር
        </p>	        </p>
      </div>	      </div>
    </div>	    </div>

src/components/code/CodeAnalyzer.tsx
+++ 22
--- 22
function ScoreRing({ score }: { score: number }) {	function ScoreRing({ score }: { score: number }) {
  const color =	  const color =
    score >= 80 ? "text-emerald-400" : score >= 60 ? "text-amber-400" : "text-red-400";	    score >= 80 ? "text-emerald-400" : score >= 60 ? "text-amber-400" : "text-red-400";
  const label = score >= 80 ? "Good" : score >= 60 ? "Fair" : "Poor";	  const label = score >= 80 ? "ጥሩ" : score >= 60 ? "ሚዛን" : "ድህነት";
  return (	  return (
    <div className="flex flex-col items-center">	    <div className="flex flex-col items-center">
      <div className={`text-4xl font-bold tabular-nums ${color}`}>{score}</div>	      <div className={`text-4xl font-bold tabular-nums ${color}`}>{score}</div>
      <div className="text-xs text-zinc-500 mt-1">Score – {label}</div>	      <div className="text-xs text-zinc-500 mt-1">ነጥብ – {label}</div>
    </div>	    </div>
  );	  );
}	}
  return (	  return (
    <div className="flex h-full flex-col">	    <div className="flex h-full flex-col">
      <div className="border-b border-zinc-800 px-6 py-4">	      <div className="border-b border-zinc-800 px-6 py-4">
        <h2 className="text-base font-semibold text-white">Code Analysis</h2>	        <h2 className="text-base font-semibold text-white">ኮድ ትንተካክል</h2>
        <p className="text-xs text-zinc-500 mt-0.5">	        <p className="text-xs text-zinc-500 mt-0.5">
          Paste your code to get instant quality, security, and performance insights	          ኮድዎን በመለጠ፣ ፈጣን ጥራት፣ ደህንነትና ብቃት ግብዓቶችን ማግኘት
        </p>	        </p>
      </div>	      </div>
 	 
            <select	            <select
              value={language}	              value={language}
              onChange={(e) => setLanguage(e.target.value)}	              onChange={(e) => setLanguage(e.target.value)}
              className="rounded-lg border border-zinc-700 bg-zinc-800 px-3 py-1.5 text-sm text-zinc-300 focus:border-violet-500 focus:outline-none"	              className="rounded-lg border border-zinc-700 bg-zinc-800 px-3 py-1.5 text-sm text-zinc-300 focus:border-green-500 focus:outline-none"
            >	            >
              {LANGUAGES.map((lang) => (	              {LANGUAGES.map((lang) => (
                <option key={lang} value={lang}>	                <option key={lang} value={lang}>
                  {lang === "auto-detect" ? "Auto-detect language" : lang}	                  {lang === "auto-detect" ? "ቋንቋ በራሱ መለየት" : lang}
                </option>	                </option>
              ))}	              ))}
            </select>	            </select>
                {isAnalyzing ? (	                {isAnalyzing ? (
                  <>	                  <>
                    <Loader2 className="h-4 w-4 animate-spin" />	                    <Loader2 className="h-4 w-4 animate-spin" />
                    Analyzing…	                    ትንተካክል…
                  </>	                  </>
                ) : (	                ) : (
                  <>	                  <>
                    <BarChart3 className="h-4 w-4" />	                    <BarChart3 className="h-4 w-4" />
                    Analyze Code	                    ኮድ ትንተካክል
                  </>	                  </>
                )}	                )}
              </Button>	              </Button>
          <textarea	          <textarea
            value={code}	            value={code}
            onChange={(e) => setCode(e.target.value)}	            onChange={(e) => setCode(e.target.value)}
            placeholder="Paste your code here…"	            placeholder="ኮድዎን እዚህ ያስገቡ…"
            className="flex-1 resize-none bg-zinc-950 p-4 font-mono text-sm text-zinc-300 placeholder-zinc-600 focus:outline-none"	            className="flex-1 resize-none bg-zinc-950 p-4 font-mono text-sm text-zinc-300 placeholder-zinc-600 focus:outline-none"
            spellCheck={false}	            spellCheck={false}
          />	          />
        <div className="w-80 overflow-y-auto bg-zinc-900">	        <div className="w-80 overflow-y-auto bg-zinc-900">
          {!result ? (	          {!result ? (
            <div className="flex h-full flex-col items-center justify-center px-6 text-center">	            <div className="flex h-full flex-col items-center justify-center px-6 text-center">
              <div className="flex h-12 w-12 items-center justify-center rounded-2xl bg-violet-600/20 border border-violet-600/30">	
                <BarChart3 className="h-6 w-6 text-violet-400" />	              <div className="flex h-12 w-12 items-center justify-center rounded-2xl bg-green-600/20 border border-green-600/30">
                <BarChart3 className="h-6 w-6 text-green-400" />
              </div>	              </div>
              <h3 className="mt-4 text-sm font-semibold text-zinc-300">	              <h3 className="mt-4 text-sm font-semibold text-zinc-300">
                Analysis Results	                የትንተካክል ውጤቶች
              </h3>	              </h3>
              <p className="mt-2 text-xs text-zinc-500">	              <p className="mt-2 text-xs text-zinc-500">
                Click &ldquo;Analyze Code&rdquo; to get detailed insights about your code quality, security, and performance.	                ስለ ኮድዎ ጥራት፣ ደህንነትና ብቃት ዝርዝር ግብዓቶችን ለማግኘት "ኮድ ትንተካክል" ጠቅ ያድርጉ።
              </p>	              </p>
            </div>	            </div>
          ) : (	          ) : (
              <div className="grid grid-cols-3 gap-2">	              <div className="grid grid-cols-3 gap-2">
                <div className="rounded-lg border border-zinc-700 bg-zinc-800 p-3 text-center">	                <div className="rounded-lg border border-zinc-700 bg-zinc-800 p-3 text-center">
                  <div className="text-lg font-bold text-white">{result.linesOfCode}</div>	                  <div className="text-lg font-bold text-white">{result.linesOfCode}</div>
                  <div className="text-xs text-zinc-500">Lines</div>	                  <div className="text-xs text-zinc-500">መስመሮች</div>
                </div>	                </div>
                <div className="rounded-lg border border-zinc-700 bg-zinc-800 p-3 text-center">	                <div className="rounded-lg border border-zinc-700 bg-zinc-800 p-3 text-center">
                  <div className="text-lg font-bold text-white capitalize">{result.complexity}</div>	                  <div className="text-lg font-bold text-white capitalize">{result.complexity}</div>
                  <div className="text-xs text-zinc-500">Complexity</div>	                  <div className="text-xs text-zinc-500">ውስብስብነት</div>
                </div>	                </div>
                <div className="rounded-lg border border-zinc-700 bg-zinc-800 p-3 text-center">	                <div className="rounded-lg border border-zinc-700 bg-zinc-800 p-3 text-center">
                  <div className="text-lg font-bold text-white">{result.issues.length}</div>	                  <div className="text-lg font-bold text-white">{result.issues.length}</div>
                  <div className="text-xs text-zinc-500">Issues</div>	                  <div className="text-xs text-zinc-500">ችግሮች</div>
                </div>	                </div>
              </div>	              </div>
 	 
              <div>	              <div>
                <h4 className="mb-2 text-xs font-semibold uppercase tracking-wider text-zinc-500">	                <h4 className="mb-2 text-xs font-semibold uppercase tracking-wider text-zinc-500">
                  Detected Language	                  የተለየው ቋንቋ
                </h4>	                </h4>
                <Badge variant="violet" className="capitalize">	                <Badge variant="green" className="capitalize">
                  {result.language}	                  {result.language}
                </Badge>	                </Badge>
              </div>	              </div>
              {result.issues.length > 0 && (	              {result.issues.length > 0 && (
                <div>	                <div>
                  <h4 className="mb-2 text-xs font-semibold uppercase tracking-wider text-zinc-500">	                  <h4 className="mb-2 text-xs font-semibold uppercase tracking-wider text-zinc-500">
                    Issues ({result.issues.length})	                    ችግሮች ({result.issues.length})
                  </h4>	                  </h4>
                  <div className="space-y-2">	                  <div className="space-y-2">
                    {result.issues.map((issue, i) => (	                    {result.issues.map((issue, i) => (
                                {issue.type}	                                {issue.type}
                              </Badge>	                              </Badge>
                              {issue.line && (	                              {issue.line && (
                                <span className="text-xs text-zinc-500">Line {issue.line}</span>	                                <span className="text-xs text-zinc-500">መስመር {issue.line}</span>
                              )}	                              )}
                            </div>	                            </div>
                            <p className="text-xs text-zinc-300">{issue.message}</p>	                            <p className="text-xs text-zinc-300">{issue.message}</p>
                            <div className="mt-1.5 flex items-start gap-1">	                            <div className="mt-1.5 flex items-start gap-1">
                              <ChevronRight className="h-3 w-3 text-violet-400 mt-0.5 shrink-0" />	                              <ChevronRight className="h-3 w-3 text-green-400 mt-0.5 shrink-0" />
                              <p className="text-xs text-zinc-500">{issue.suggestion}</p>	                              <p className="text-xs text-zinc-500">{issue.suggestion}</p>
                            </div>	                            </div>
                          </div>	                          </div>
              {result.suggestions.length > 0 && (	              {result.suggestions.length > 0 && (
                <div>	                <div>
                  <h4 className="mb-2 text-xs font-semibold uppercase tracking-wider text-zinc-500">	                  <h4 className="mb-2 text-xs font-semibold uppercase tracking-wider text-zinc-500">
                    Suggestions	                    ድርሰቶች
                  </h4>	                  </h4>
                  <div className="space-y-2">	                  <div className="space-y-2">
                    {result.suggestions.map((suggestion, i) => (	                    {result.suggestions.map((suggestion, i) => (

src/components/layout/Sidebar.tsx
+++ 10
--- 10
}	}
 	 
const navItems = [	const navItems = [
  { id: "chat" as ActiveTab, label: "Chat", icon: MessageSquare },	
  { id: "code" as ActiveTab, label: "Code Analysis", icon: Code2 },	
  { id: "tasks" as ActiveTab, label: "Task Planner", icon: CheckSquare },	  { id: "chat" as ActiveTab, label: "ትርጉም", icon: MessageSquare },
  { id: "code" as ActiveTab, label: "ኮድ ትንተካክል", icon: Code2 },
  { id: "tasks" as ActiveTab, label: "ተግባር አስተዳደር", icon: CheckSquare },
];	];
 	 
export function Sidebar({ activeTab, onTabChange }: SidebarProps) {	export function Sidebar({ activeTab, onTabChange }: SidebarProps) {
  return (	  return (
    <aside className="flex h-full w-64 flex-col border-r border-zinc-800 bg-zinc-950">	    <aside className="flex h-full w-64 flex-col border-r border-zinc-800 bg-zinc-950">
      <div className="flex items-center gap-2.5 border-b border-zinc-800 px-4 py-4">	      <div className="flex items-center gap-2.5 border-b border-zinc-800 px-4 py-4">
        <div className="flex h-8 w-8 items-center justify-center rounded-lg bg-violet-600">	        <div className="flex h-8 w-8 items-center justify-center rounded-lg bg-gradient-to-br from-green-500 via-yellow-500 to-red-500">
          <Bot className="h-4 w-4 text-white" />	          <Bot className="h-4 w-4 text-white" />
        </div>	        </div>
        <div>	        <div>
          <h1 className="text-sm font-bold text-white">DevAI Assistant</h1>	
          <p className="text-xs text-zinc-500">AI-powered coding</p>	          <h1 className="text-sm font-bold text-white">የኢትዮጵያ AI ረዳት</h1>
          <p className="text-xs text-zinc-500">ኢትዮጵያ ለኢትዮጵያ</p>
        </div>	        </div>
      </div>	      </div>
 	 
            onClick={() => onTabChange(id)}	            onClick={() => onTabChange(id)}
            className={`mb-1 flex w-full items-center gap-3 rounded-lg px-3 py-2.5 text-sm font-medium transition-colors ${	            className={`mb-1 flex w-full items-center gap-3 rounded-lg px-3 py-2.5 text-sm font-medium transition-colors ${
              activeTab === id	              activeTab === id
                ? "bg-violet-600/20 text-violet-400"	                ? "bg-green-600/20 text-green-400"
                : "text-zinc-400 hover:bg-zinc-800 hover:text-zinc-200"	                : "text-zinc-400 hover:bg-zinc-800 hover:text-zinc-200"
            }`}	            }`}
          >	          >
      <div className="flex flex-col flex-1 overflow-hidden px-3 py-3">	      <div className="flex flex-col flex-1 overflow-hidden px-3 py-3">
        <div className="mb-3 flex items-center justify-between">	        <div className="mb-3 flex items-center justify-between">
          <span className="text-xs font-semibold uppercase tracking-wider text-zinc-500">	          <span className="text-xs font-semibold uppercase tracking-wider text-zinc-500">
            Conversations	            ውይይቶች
          </span>	          </span>
          <Button size="sm" variant="ghost" onClick={handleNewChat} className="h-6 w-6 p-0">	          <Button size="sm" variant="ghost" onClick={handleNewChat} className="h-6 w-6 p-0">
            <Plus className="h-3.5 w-3.5" />	            <Plus className="h-3.5 w-3.5" />
 	 
        <div className="flex-1 overflow-y-auto space-y-0.5">	        <div className="flex-1 overflow-y-auto space-y-0.5">
          {conversations.length === 0 ? (	          {conversations.length === 0 ? (
            <p className="px-2 text-xs text-zinc-600 italic">No conversations yet</p>	            <p className="px-2 text-xs text-zinc-600 italic">ገና ምንም ውይይት የለም</p>
          ) : (	          ) : (
            conversations.map((conv) => (	            conversations.map((conv) => (
              <div	              <div
 	 
      <div className="border-t border-zinc-800 px-4 py-3">	      <div className="border-t border-zinc-800 px-4 py-3">
        <p className="text-xs text-zinc-600 text-center">	        <p className="text-xs text-zinc-600 text-center">
          AI responses are simulated	          ምላሾች የተሳሉ ናቸው
        </p>	        </p>
      </div>	      </div>
    </aside>	    </aside>

src/components/tasks/AddTaskModal.tsx
+++ 24
--- 24
    <div className="fixed inset-0 z-50 flex items-center justify-center bg-black/60 backdrop-blur-sm">	    <div className="fixed inset-0 z-50 flex items-center justify-center bg-black/60 backdrop-blur-sm">
      <div className="w-full max-w-md rounded-2xl border border-zinc-700 bg-zinc-900 shadow-2xl">	      <div className="w-full max-w-md rounded-2xl border border-zinc-700 bg-zinc-900 shadow-2xl">
        <div className="flex items-center justify-between border-b border-zinc-700 px-5 py-4">	        <div className="flex items-center justify-between border-b border-zinc-700 px-5 py-4">
          <h3 className="text-sm font-semibold text-white">Add New Task</h3>	          <h3 className="text-sm font-semibold text-white">አዲስ ተግባር ጨምር</h3>
          <button	          <button
            onClick={onClose}	            onClick={onClose}
            className="flex h-7 w-7 items-center justify-center rounded-lg text-zinc-500 hover:bg-zinc-800 hover:text-zinc-300 transition-colors"	            className="flex h-7 w-7 items-center justify-center rounded-lg text-zinc-500 hover:bg-zinc-800 hover:text-zinc-300 transition-colors"
        <form onSubmit={handleSubmit} className="p-5 space-y-4">	        <form onSubmit={handleSubmit} className="p-5 space-y-4">
          <div>	          <div>
            <label className="mb-1.5 block text-xs font-medium text-zinc-400">	            <label className="mb-1.5 block text-xs font-medium text-zinc-400">
              Task Title <span className="text-red-400">*</span>	              ተግባር ርእስ <span className="text-red-400">*</span>
            </label>	            </label>
            <input	            <input
              type="text"	              type="text"
              value={title}	              value={title}
              onChange={(e) => setTitle(e.target.value)}	              onChange={(e) => setTitle(e.target.value)}
              placeholder="Enter task title"	
              className="w-full rounded-lg border border-zinc-700 bg-zinc-800 px-3 py-2 text-sm text-zinc-100 placeholder-zinc-500 focus:border-violet-500 focus:outline-none focus:ring-1 focus:ring-violet-500"	              placeholder="የተግባር ርእስ ያስገቡ"
              className="w-full rounded-lg border border-zinc-700 bg-zinc-800 px-3 py-2 text-sm text-zinc-100 placeholder-zinc-500 focus:border-green-500 focus:outline-none focus:ring-1 focus:ring-green-500"
              required	              required
              autoFocus	              autoFocus
            />	            />
 	 
          <div>	          <div>
            <label className="mb-1.5 block text-xs font-medium text-zinc-400">	            <label className="mb-1.5 block text-xs font-medium text-zinc-400">
              Description	              ገለፃ
            </label>	            </label>
            <textarea	            <textarea
              value={description}	              value={description}
              onChange={(e) => setDescription(e.target.value)}	              onChange={(e) => setDescription(e.target.value)}
              placeholder="Describe the task…"	              placeholder="ተግባሩን ገልፁ…"
              rows={3}	              rows={3}
              className="w-full resize-none rounded-lg border border-zinc-700 bg-zinc-800 px-3 py-2 text-sm text-zinc-100 placeholder-zinc-500 focus:border-violet-500 focus:outline-none focus:ring-1 focus:ring-violet-500"	              className="w-full resize-none rounded-lg border border-zinc-700 bg-zinc-800 px-3 py-2 text-sm text-zinc-100 placeholder-zinc-500 focus:border-green-500 focus:outline-none focus:ring-1 focus:ring-green-500"
            />	            />
          </div>	          </div>
 	 
          <div className="grid grid-cols-2 gap-3">	          <div className="grid grid-cols-2 gap-3">
            <div>	            <div>
              <label className="mb-1.5 block text-xs font-medium text-zinc-400">Priority</label>	              <label className="mb-1.5 block text-xs font-medium text-zinc-400">ቅድሚያ</label>
              <select	              <select
                value={priority}	                value={priority}
                onChange={(e) => setPriority(e.target.value as TaskPriority)}	                onChange={(e) => setPriority(e.target.value as TaskPriority)}
                className="w-full rounded-lg border border-zinc-700 bg-zinc-800 px-3 py-2 text-sm text-zinc-300 focus:border-violet-500 focus:outline-none"	                className="w-full rounded-lg border border-zinc-700 bg-zinc-800 px-3 py-2 text-sm text-zinc-300 focus:border-green-500 focus:outline-none"
              >	              >
                <option value="low">Low</option>	
                <option value="medium">Medium</option>	
                <option value="high">High</option>	                <option value="low">ዝቅተኛ</option>
                <option value="medium">መካከለኛ</option>
                <option value="high">ከፍተኛ</option>
              </select>	              </select>
            </div>	            </div>
            <div>	            <div>
              <label className="mb-1.5 block text-xs font-medium text-zinc-400">Status</label>	              <label className="mb-1.5 block text-xs font-medium text-zinc-400">ሁኔታ</label>
              <select	              <select
                value={status}	                value={status}
                onChange={(e) => setStatus(e.target.value as TaskStatus)}	                onChange={(e) => setStatus(e.target.value as TaskStatus)}
                className="w-full rounded-lg border border-zinc-700 bg-zinc-800 px-3 py-2 text-sm text-zinc-300 focus:border-violet-500 focus:outline-none"	                className="w-full rounded-lg border border-zinc-700 bg-zinc-800 px-3 py-2 text-sm text-zinc-300 focus:border-green-500 focus:outline-none"
              >	              >
                <option value="todo">To Do</option>	
                <option value="in-progress">In Progress</option>	
                <option value="done">Done</option>	                <option value="todo">ሊያደርጉ</option>
                <option value="in-progress">በማድረግ</option>
                <option value="done">ተጠናቋል</option>
              </select>	              </select>
            </div>	            </div>
          </div>	          </div>
          <div className="grid grid-cols-2 gap-3">	          <div className="grid grid-cols-2 gap-3">
            <div>	            <div>
              <label className="mb-1.5 block text-xs font-medium text-zinc-400">	              <label className="mb-1.5 block text-xs font-medium text-zinc-400">
                Estimated Hours	                ተብራርቶ ሰአቶች
              </label>	              </label>
              <input	              <input
                type="number"	                type="number"
                value={estimatedHours}	                value={estimatedHours}
                onChange={(e) => setEstimatedHours(e.target.value)}	                onChange={(e) => setEstimatedHours(e.target.value)}
                placeholder="e.g. 4"	                placeholder="ለምሳሌ 4"
                min="0.5"	                min="0.5"
                step="0.5"	                step="0.5"
                className="w-full rounded-lg border border-zinc-700 bg-zinc-800 px-3 py-2 text-sm text-zinc-100 placeholder-zinc-500 focus:border-violet-500 focus:outline-none"	                className="w-full rounded-lg border border-zinc-700 bg-zinc-800 px-3 py-2 text-sm text-zinc-100 placeholder-zinc-500 focus:border-green-500 focus:outline-none focus:ring-1 focus:ring-green-500"
              />	              />
            </div>	            </div>
            <div>	            <div>
              <label className="mb-1.5 block text-xs font-medium text-zinc-400">	              <label className="mb-1.5 block text-xs font-medium text-zinc-400">
                Tags (comma-separated)	                ቲጋዎች (በካምያ ይለያያሉ)
              </label>	              </label>
              <input	              <input
                type="text"	                type="text"
                value={tags}	                value={tags}
                onChange={(e) => setTags(e.target.value)}	                onChange={(e) => setTags(e.target.value)}
                placeholder="api, frontend"	                placeholder="api, frontend"
                className="w-full rounded-lg border border-zinc-700 bg-zinc-800 px-3 py-2 text-sm text-zinc-100 placeholder-zinc-500 focus:border-violet-500 focus:outline-none"	                className="w-full rounded-lg border border-zinc-700 bg-zinc-800 px-3 py-2 text-sm text-zinc-100 placeholder-zinc-500 focus:border-green-500 focus:outline-none focus:ring-1 focus:ring-green-500"
              />	              />
            </div>	            </div>
          </div>	          </div>
 	 
          <div className="flex gap-3 pt-1">	          <div className="flex gap-3 pt-1">
            <Button type="button" variant="secondary" onClick={onClose} className="flex-1">	            <Button type="button" variant="secondary" onClick={onClose} className="flex-1">
              Cancel	              ይቁም
            </Button>	            </Button>
            <Button type="submit" className="flex-1" disabled={!title.trim()}>	            <Button type="submit" className="flex-1" disabled={!title.trim()}>
              Add Task	              ተግባር ጨምር
            </Button>	            </Button>
          </div>	          </div>
        </form>	        </form>

src/components/tasks/TaskPlanner.tsx
+++ 11
--- 11
import { Button } from "@/components/ui/Button";	import { Button } from "@/components/ui/Button";
 	 
const COLUMNS: { id: TaskStatus; label: string; icon: React.ElementType; color: string }[] = [	const COLUMNS: { id: TaskStatus; label: string; icon: React.ElementType; color: string }[] = [
  { id: "todo", label: "To Do", icon: Circle, color: "text-zinc-400" },	
  { id: "in-progress", label: "In Progress", icon: Loader, color: "text-blue-400" },	
  { id: "done", label: "Done", icon: CheckCircle2, color: "text-emerald-400" },	  { id: "todo", label: "ሊያደርጉ", icon: Circle, color: "text-zinc-400" },
  { id: "in-progress", label: "በማድረግ", icon: Loader, color: "text-blue-400" },
  { id: "done", label: "ተጠናቋል", icon: CheckCircle2, color: "text-emerald-400" },
];	];
 	 
export function TaskPlanner() {	export function TaskPlanner() {
        <div className="flex items-center justify-between">	        <div className="flex items-center justify-between">
          <div>	          <div>
            <h2 className="text-base font-semibold text-white">	            <h2 className="text-base font-semibold text-white">
              {activeProject?.name ?? "Task Planner"}	              {activeProject?.name ?? "ተግባር አስተዳደር"}
            </h2>	            </h2>
            <p className="text-xs text-zinc-500 mt-0.5">	            <p className="text-xs text-zinc-500 mt-0.5">
              {tasks.length} tasks · {totalHours}h total · {progress}% complete	              {tasks.length} ተግባራት · {totalHours}ሰአት ጠቅላላ · {progress}% ተጠናቋል
            </p>	            </p>
          </div>	          </div>
          <Button onClick={() => setShowAddModal(true)} size="sm">	          <Button onClick={() => setShowAddModal(true)} size="sm">
            <Plus className="h-4 w-4" />	            <Plus className="h-4 w-4" />
            Add Task	            ተግባር ጨምር
          </Button>	          </Button>
        </div>	        </div>
 	 
        <div className="mt-3">	        <div className="mt-3">
          <div className="flex items-center justify-between mb-1">	          <div className="flex items-center justify-between mb-1">
            <span className="text-xs text-zinc-500">Progress</span>	            <span className="text-xs text-zinc-500">ሂደት</span>
            <span className="text-xs text-zinc-400 font-medium">{progress}%</span>	            <span className="text-xs text-zinc-400 font-medium">{progress}%</span>
          </div>	          </div>
          <div className="h-1.5 rounded-full bg-zinc-800 overflow-hidden">	          <div className="h-1.5 rounded-full bg-zinc-800 overflow-hidden">
            <div	            <div
              className="h-full rounded-full bg-violet-600 transition-all duration-500"	              className="h-full rounded-full bg-green-600 transition-all duration-500"
              style={{ width: `${progress}%` }}	              style={{ width: `${progress}%` }}
            />	            />
          </div>	          </div>
                  {columnTasks.length === 0 ? (	                  {columnTasks.length === 0 ? (
                    <div className="flex flex-col items-center justify-center rounded-xl border border-dashed border-zinc-700 py-8 text-center">	                    <div className="flex flex-col items-center justify-center rounded-xl border border-dashed border-zinc-700 py-8 text-center">
                      <CheckSquare className="h-8 w-8 text-zinc-700 mb-2" />	                      <CheckSquare className="h-8 w-8 text-zinc-700 mb-2" />
                      <p className="text-xs text-zinc-600">No tasks here</p>	                      <p className="text-xs text-zinc-600">ተግባር የለም</p>
                    </div>	                    </div>
                  ) : (	                  ) : (
                    columnTasks.map((task) => (	                    columnTasks.map((task) => (
 	 
                <button	                <button
                  onClick={() => setShowAddModal(true)}	                  onClick={() => setShowAddModal(true)}
                  className="mt-3 flex items-center gap-2 rounded-xl border border-dashed border-zinc-700 px-4 py-2.5 text-xs text-zinc-500 transition-colors hover:border-violet-600/50 hover:text-violet-400"	                  className="mt-3 flex items-center gap-2 rounded-xl border border-dashed border-zinc-700 px-4 py-2.5 text-xs text-zinc-500 transition-colors hover:border-green-600/50 hover:text-green-400"
                >	                >
                  <Plus className="h-3.5 w-3.5" />	                  <Plus className="h-3.5 w-3.5" />
                  Add task	                  ተግባር ጨምር
                </button>	                </button>
              </div>	              </div>
            );	            );

src/components/ui/Badge.tsx
+++ 2
--- 1
 	 
interface BadgeProps {	interface BadgeProps {
  children: ReactNode;	  children: ReactNode;
  variant?: "default" | "success" | "warning" | "danger" | "info" | "violet";	  variant?: "default" | "success" | "warning" | "danger" | "info" | "violet" | "green";
  className?: string;	  className?: string;
}	}
 	 
  danger: "bg-red-900/50 text-red-400 border border-red-800",	  danger: "bg-red-900/50 text-red-400 border border-red-800",
  info: "bg-blue-900/50 text-blue-400 border border-blue-800",	  info: "bg-blue-900/50 text-blue-400 border border-blue-800",
  violet: "bg-violet-900/50 text-violet-400 border border-violet-800",	  violet: "bg-violet-900/50 text-violet-400 border border-violet-800",
  green: "bg-green-900/50 text-green-400 border border-green-800",
};	};
 	 
export function Badge({ children, variant = "default", className = "" }: BadgeProps) {	export function Badge({ children, variant = "default", className = "" }: BadgeProps) {
