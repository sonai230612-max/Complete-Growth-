import { Link, useRouterState } from "@tanstack/react-router";  
import type { ReactNode } from "react";  
import { user } from "@/lib/demo-data";  
import { usePro } from "@/lib/pro-context";  
  
const tabs = [  
  { to: "/", label: "Home" },  
  { to: "/explore", label: "Explore" },  
  { to: "/results", label: "Results" },  
  { to: "/feedback", label: "Feedback" },  
  { to: "/progress", label: "Progress" },  
] as const;  
  
export function AppShell({ children }: { children: ReactNode }) {  
  const pathname = useRouterState({ select: (s) => s.location.pathname });  
  const { isPro, source } = usePro();  
  
  return (  
    <div className="relative min-h-screen w-full overflow-x-hidden bg-ink font-body text-foreground">  
      <div className="pointer-events-none fixed inset-0">  
        <div className="absolute -left-16 -top-24 size-72 rounded-full bg-accent/20 blur-[90px]" />  
        <div className="absolute -right-20 top-40 size-72 rounded-full bg-accent-2/15 blur-[90px]" />  
        <div className="absolute bottom-0 left-1/3 size-64 rounded-full bg-amber/10 blur-[80px]" />  
      </div>  
  
      <div className="relative mx-auto flex min-h-screen w-full max-w-[420px] flex-col px-5 pb-32 pt-6">  
        <header className="grid grid-cols-[minmax(0,1fr)_auto] items-center gap-4">  
          <Link to="/" className="flex min-w-0 items-center gap-2.5">  
            <div className="grid size-9 shrink-0 place-items-center rounded-xl bg-gradient-to-br from-accent to-accent-2 font-display text-sm font-semibold text-ink">  
              C  
            </div>  
            <div className="min-w-0 leading-none">  
              <p className="truncate font-display text-[15px] font-semibold tracking-tight">  
                Compete&amp;Grow  
              </p>  
              <p className="mt-1 truncate text-[10px] uppercase tracking-[0.18em] text-mist-2">  
                Don&apos;t just compete. Grow.  
              </p>  
            </div>  
          </Link>  
          <div className="flex shrink-0 items-center gap-2">  
            {isPro ? (  
              <span className="rounded-full bg-accent/15 px-2 py-0.5 text-[10px] font-semibold uppercase tracking-[0.14em] text-accent">  
                Pro  
              </span>  
            ) : null}  
            <div className="grid size-9 place-items-center rounded-full bg-white/5 text-[11px] font-semibold text-mist ring-1 ring-white/10">  
              {user.initial}  
            </div>  
          </div>  
        </header>  
  
        {source === "judge-test-mode" ? (  
          <div className="mt-4 rounded-xl bg-amber/10 px-3 py-2 ring-1 ring-amber/30">  
            <p className="text-[11px] font-medium text-amber">  
              Judge Test Mode active — Pro unlocked for evaluation. No payment was taken.  
            </p>  
          </div>  
        ) : null}  
  
        <main className="flex-1">{children}</main>  
      </div>  
  
      <nav className="fixed bottom-0 left-1/2 w-full max-w-[420px] -translate-x-1/2 px-5 pb-4">  
        <div className="flex items-center justify-between rounded-[20px] bg-ink-2/85 px-3 py-2.5 ring-1 ring-white/10 backdrop-blur-xl">  
          {tabs.map((tab) => {  
            const active = tab.to === "/" ? pathname === "/" : pathname.startsWith(tab.to);  
            return (  
              <Link  
                key={tab.to}  
                to={tab.to}  
                className={`flex flex-col items-center gap-1 ${active ? "text-accent" : "text-mist-2"}`}  
              >  
                <span className="text-[13px] leading-none">{tab.label}</span>  
                <span  
                  className={`h-1 w-1 rounded-full ${active ? "bg-accent" : "bg-transparent"}`}  
                />  
              </Link>  
            );  
          })}  
        </div>  
      </nav>  
    </div>  
  );  
}  
  
export function SectionHeading({  
  title,  
  meta,  
  className = "",  
}: {  
  title: string;  
  meta?: string;  
  className?: string;  
}) {  
  return (  
    <div className={`flex items-center justify-between gap-3 ${className}`}>  
      <h2 className="min-w-0 truncate font-display text-[15px] font-semibold tracking-tight">  
        {title}  
      </h2>  
      {meta ? <span className="shrink-0 text-[11px] font-medium text-mist-2">{meta}</span> : null}  
    </div>  
  );  
}  
  
export function Eyebrow({ children }: { children: ReactNode }) {  
  return (  
    <p className="text-[11px] font-medium uppercase tracking-[0.16em] text-mist-2">{children}</p>  
  );  
}  
  
export function GlassCard({  
  children,  
  className = "",  
  delay = 0,  
}: {  
  children: ReactNode;  
  className?: string;  
  delay?: number;  
}) {  
  return (  
    <section  
      className={`cg-rise rounded-[20px] glass p-4 ring-1 ring-white/10 ${className}`}  
      style={{ animationDelay: `${delay}s` }}  
    >  
      {children}  
    </section>  
  );  
}  
